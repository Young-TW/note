# ROCm LMCache Redis 設定

測試過程中發現 Redis 預設的 `proto-max-bulk-len` 參數過小，導致在進行大批次寫入時出現錯誤。因此需要調整 Redis 的啟動參數來增加此限制。

```yaml
services:
  redis:
    image: redis:alpine
    container_name: lmcache_redis
    network_mode: host
    command: redis-server --proto-max-bulk-len 1073741824 --save "" --appendonly no
```

重啟後透過 Python 腳本確認寫入成功

```py
import redis
import torch
import io
import time

# Configuration - ensure these match your docker-compose or env vars
REDIS_HOST = 'localhost'  # Or 'localhost' / IP, depending on where you run this script
REDIS_PORT = 6379
TEST_KEY = "lmcache:test_kv"

def test_redis_write_read():
    try:
        # 1. Connect to Redis
        print(f"Connecting to Redis at {REDIS_HOST}:{REDIS_PORT}...")
        client = redis.Redis(host=REDIS_HOST, port=REDIS_PORT, db=0)

        if not client.ping():
            print("Error: Could not ping Redis.")
            return

        print("Redis connected successfully.")

        # 2. Simulate KV Cache Data (PyTorch Tensor)
        # Create a dummy tensor representing KV cache
        # dummy_tensor = torch.randn(1, 32, 128, 128)
        dummy_tensor = torch.randn(1, 32, 128, 32768)
        print(f"Generated dummy tensor: {dummy_tensor.shape}")

        # 3. Serialize (Simulating LMCache logic)
        # Most implementations use torch.save to a buffer or pickle
        buffer = io.BytesIO()
        torch.save(dummy_tensor, buffer)
        binary_data = buffer.getvalue()

        data_size_mb = len(binary_data) / (1024 * 1024)
        print(f"Serialized data size: {data_size_mb:.2f} MB")

        # 4. Write to Redis
        start_time = time.time()
        client.set(TEST_KEY, binary_data)
        # Optionally set an expire time to avoid clogging memory
        client.expire(TEST_KEY, 60)
        print(f"Write successful! Time taken: {time.time() - start_time:.4f}s")

        # 5. Read back verification
        retrieved_data = client.get(TEST_KEY)
        if retrieved_data:
            read_buffer = io.BytesIO(retrieved_data)
            loaded_tensor = torch.load(read_buffer)
            print("Read back successful. Tensor shape matches:", loaded_tensor.shape)
        else:
            print("Error: Key not found after writing.")

    except Exception as e:
        print(f"Exception occurred: {e}")

if __name__ == "__main__":
    test_redis_write_read()
```
