# Llama3.1-70B-Instruct ROCm 環境基準測試結果

### 測試一：Llama3.1-70B-Instruct 模型在 ROCm 環境下的吞吐量

```sh
vllm bench throughput \
    --model meta-llama/Llama-3.1-70B-Instruct \
    --tensor-parallel-size 1 \
    --input-len 256 \
    --output-len 256 \
    --num-prompts 1000 \
    --dtype auto
```

```txt
Throughput: 5.35 requests/s, 2735.50 total tokens/s, 1369.41 output tokens/s
Total num prompt tokens:  255378
Total num output tokens:  256000
```

### 測試二：Llama3.1-70B-Instruct 模型在 ROCm 環境下的延遲

```sh
vllm bench latency \
    --model meta-llama/Llama-3.1-70B-Instruct \
    --tensor-parallel-size 1 \
    --input-len 256 \
    --output-len 128 \
    --batch-size 8 \
    --num-iters-warmup 10 \
    --num-iters 100
```

```txt
Avg latency: 5.2564156893700105 seconds
10% percentile latency: 5.241361258600318 seconds
25% percentile latency: 5.248211075249856 seconds
50% percentile latency: 5.258143185500103 seconds
75% percentile latency: 5.265569431749896 seconds
90% percentile latency: 5.269668612399892 seconds
99% percentile latency: 5.273114479820046 seconds
```
