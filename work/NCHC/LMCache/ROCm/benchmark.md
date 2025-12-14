# vLLM & LMCache ROCm 環境下的效能基準測試

## 硬體環境

```txt
CPU: AMD EPYC 9654 *2
GPU: AMD MI325X *8 # 因為還沒重新斷電冷啟動所以 GPU 載入只有四張
RAM: 2.3TB
```

## 軟體測試

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

### 測試三：啟動 LMCache 伺服器

安裝 git 並下載 LMCache 原始碼

```sh
apt-get update && apt-get install -y git

git clone https://github.com/LMCache/LMCache.git
cd LMCache
```

編譯並安裝 LMCache，MI325X 架構通常相容於 gfx942

```sh
export PYTORCH_ROCM_ARCH="gfx942"
export TORCH_DONT_CHECK_COMPILER_ABI=1
export CXX=hipcc
export BUILD_WITH_HIP=1

python3 -m pip install --no-build-isolation -e .
```

啟動 LMCache

```sh
LMCACHE_CHUNK_SIZE=256 \
vllm serve Qwen/Qwen3-8B \
    --port 8000 \
    --tensor-parallel-size 1 \
    --kv-transfer-config '{"kv_connector":"LMCacheConnectorV1", "kv_role":"kv_both"}'
```
