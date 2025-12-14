# vLLM & LMCache ROCm 環境下的效能基準測試

## 硬體環境

```txt
CPU: AMD EPYC 9654 *2
GPU: AMD MI325X *8 # 因為還沒重新斷電冷啟動所以 GPU 載入只有四張
RAM: 2.3TB
```

### 測試一：Qwen3-8B 模型在 ROCm 環境下的吞吐量

```sh
vllm bench throughput \
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

### 測試二：Qwen2-7B-Instruct 模型在 ROCm 環境下的延遲

```sh
vllm bench latency \
    --model Qwen/Qwen3-8B \
    --tensor-parallel-size 1 \
    --input-len 256 \
    --output-len 128 \
    --batch-size 8 \
    --num-iters-warmup 10 \
    --num-iters 100
```

#### 結果

```txt
Avg latency: 1.475279240796808 seconds
10% percentile latency: 1.4704144389019347 seconds
25% percentile latency: 1.4711670397227863 seconds
50% percentile latency: 1.4726597834960558 seconds
75% percentile latency: 1.4755478004954057 seconds
90% percentile latency: 1.4805126614111943 seconds
99% percentile latency: 1.5062954947334948 seconds
```
