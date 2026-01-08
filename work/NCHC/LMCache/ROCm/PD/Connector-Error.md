# ROCm LMCache Connector 錯誤

當 ROCm LMCache 的 Connector 連接 Redis 在進行批次寫入（batched put）操作時，印出的 Error Log 如下：

```sh
lmcache_producer  | (EngineCore_DP0 pid=719) [2026-01-08 16:41:10,987] LMCache WARNING: batched put error: zip() argument 2 is shorter than argument 1 (instrumented_connector.py:118:lmcache.v1.storage_backend.connector.instrumented_connector)
```

因此 Redis 為空，導致 Decode 節點無法從 Redis 讀取到任何 KV Cache。

## 問題原因

經過調查，發現問題出在 `instrumented_connector.py` 中的 `batched_put` 方法。該方法在執行 `zip(keys, memory_objs)` 時，假設 `keys` 和 `memory_objs` 的長度相同，但實際上可能會出現不匹配的情況，導致 `zip` 函數拋出錯誤。

原始[程式碼](https://github.com/LMCache/LMCache/blob/829b5c8985d5d944582f7f54ede0d7d1f81cbe6b/lmcache/v1/storage_backend/connector/instrumented_connector.py)：

```py
async def batched_put(
    self, keys: List[CacheEngineKey], memory_objs: List[MemoryObj]
):
    total_size = sum(
        memory_obj.get_size()
        for memory_obj in memory_objs
        if memory_obj is not None
    )
    begin = time.perf_counter()
    try:
        await self._connector.batched_put(keys, memory_objs)
    except Exception as e:
        logger.warning(f"batched put error: {e}")
    finally:
        for memory_obj in memory_objs:
            memory_obj.ref_count_down()

    end = time.perf_counter()
    self._stats_monitor.update_interval_remote_time_to_put((end - begin) * 1000)
    self._stats_monitor.update_interval_remote_write_metrics(total_size)
    logger.debug(
        "[%s]Bytes offloaded: %.3f MBytes in %.3f ms",
        self.name,
        total_size / 1e6,
        (end - begin) * 1000,
    )
```

修正的版本如下：

```py
async def batched_put(
    self, keys: List[CacheEngineKey], memory_objs: List[MemoryObj]
):
    keys_to_put = keys
    objs_to_put = memory_objs

    if len(keys) != len(memory_objs):
        logger.warning(
            f"Length mismatch in batched_put: keys={len(keys)}, objs={len(memory_objs)}. "
            "Truncating to minimum length."
        )
        min_len = min(len(keys), len(memory_objs))
        keys_to_put = keys[:min_len]
        objs_to_put = memory_objs[:min_len]

    total_size = sum(
        memory_obj.get_size()
        for memory_obj in objs_to_put
        if memory_obj is not None
    )

    begin = time.perf_counter()
    try:
        await self._connector.batched_put(keys_to_put, objs_to_put)
    except Exception as e:
        logger.warning(f"batched put error: {e}")
    finally:
        for memory_obj in memory_objs:
            memory_obj.ref_count_down()

    end = time.perf_counter()
    self._stats_monitor.update_interval_remote_time_to_put((end - begin) * 1000)
    self._stats_monitor.update_interval_remote_write_metrics(total_size)
    logger.debug(
        "[%s]Bytes offloaded: %.3f MBytes in %.3f ms",
        self.name,
        total_size / 1e6,
        (end - begin) * 1000,
    )
```

這樣改動的預期是解決 `zip` 長度不匹配的問題，避免錯誤發生，並確保 Redis 能夠正確接收批次寫入的資料。
但目前還沒上機實測。
