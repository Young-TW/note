# vLLM & LMCache ROCm 環境下的效能基準測試

## 硬體環境

```txt
CPU: AMD EPYC 9654 *2
GPU: AMD MI325X *8 # 因為還沒重新斷電冷啟動所以 GPU 載入只有四張
RAM: 2.3TB
```

### 測試一：透過 vLLM 的 benchmark 工具測試 Qwen3-8B 模型在 ROCm 環境下的吞吐量。

```sh
root@agpn04:/app# vllm bench throughput \
    --model Qwen/Qwen3-8B \
    --tensor-parallel-size 1 \
    --input-len 256 \
    --output-len 256 \
    --num-prompts 1000 \
    --dtype auto
```

#### 結果

```txt
Throughput: 34.14 requests/s, 17466.30 total tokens/s, 8739.16 output tokens/s
Total num prompt tokens:  255648
Total num output tokens:  256000
```
