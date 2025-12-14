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

#### 測試過程

```txt
INFO:     Started server process [5196]
INFO:     Waiting for application startup.
INFO:     Application startup complete.
```

##### 請求 vLLM 伺服器

```sh
curl http://localhost:8000/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "Qwen/Qwen3-8B",
    "messages": [
      {"role": "system", "content": "你是一個樂於助人的助手。"},
      {"role": "user", "content": "請用一句話解釋什麼是 KV Cache？"}
    ],
    "max_tokens": 100,
    "temperature": 0.7
  }'
```

##### vLLM 回應

```json
{
  "id": "chatcmpl-0ab9cd7c72b04bb49c4a731440f236e7",
  "object": "chat.completion",
  "created": 1765727855,
  "model": "Qwen/Qwen3-8B",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "reasoning_content": null,
        "content": "<think>\n好的，用户让我用一句话解释什么是KV Cache。首先，我需要确认自己对KV Cache的理解是否正确。KV Cache，也就是键值缓存，通常在处理序列数据时使用，比如在Transformer模型中。在解码过程中，模型需要记住之前处理过的输入，以便在生成后续输出时能够正确地进行上下文关联。KV Cache的作用就是存储这些键和值，这样在每次生成新的token时，模型不需要重新计算之前的键",
        "tool_calls": []
      },
      "logprobs": null,
      "finish_reason": "length",
      "stop_reason": null
    }
  ],
  "usage": {
    "prompt_tokens": 31,
    "total_tokens": 131,
    "completion_tokens": 100,
    "prompt_tokens_details": null
  },
  "prompt_logprobs": null,
  "kv_transfer_params": null
}
```

##### 多次請求並觀察 LMCache 作用

設計一個長篇提示詞來測試 LMCache 的效果：

```sh
#!/bin/bash

LONG_PROMPT="在 Shell Wrapper 的情境下,\`stdin\` 之所以「幾乎總是」被視為 Blocking IO(或表現得像 Blocking),主要有三個層面的原因d:
###1. 作業系統的預設行為 (The Default)在 Linux/Unix 中,所有的 File Descriptor(包含 \`stdin\`)預設都是 Blocking 的。
 行為d:  當你呼叫 \`read(stdin, buffer, size)\` 時,如果使用者沒有輸入任何東西,程式就會停在那一行(Hang/Sleep),直到有資料進來為止。
 為什麼這樣設計？ 這是最節省 CPU 的方式。如果沒有輸入,作業系統就把你的程式掛起(Suspend),讓 CPU 去做別的事。
 Wrapper 的困境d:  如果您寫一個 Wrapper,既要監聽使用者的鍵盤輸入,又要監聽後端程式(如 Shell)的輸出,單純的 Blocking \`read\` 就會出事 —— 因為你卡在等鍵盤時,後端程式可能有輸出要印,結果因為你卡住而印不出來(Deadlock 或延遲)。
###2. TTY 的「行緩衝」模式 (Canonical Mode)這點最常被忽略。Shell Wrapper 通常是跑在 Terminal (TTY) 裡的。Terminal 預設處於 Canonical Mode(標準模式)。
 現象d:  即使你寫了程式去讀 \`stdin\`,使用者打字時,資料不會立刻傳給你的程式。資料會先被 TTY 的 Line Discipline(行規程)攔截並暫存。
 直到按下 Enterd:  只有當使用者按下 \`Enter\` 鍵,OS 才會把整行資料「推」給你的 \`stdin\`。
 這就是一種 Blockingd:  在使用者按 Enter 之前,對你的程式來說,\`stdin\` 就是空的、讀不到東西的。這是一種物理層級的 Blocking。
 註: 要做到像自動補全(Auto-suggestion)那樣逐字讀取,必須把 TTY 設為 Raw Mode,這又增加了實作複雜度。
"

python3 -c "import json, sys;
print(json.dumps({
    'model': 'Qwen/Qwen3-8B',
    'messages': [
        {'role': 'system', 'content': '你是一個摘要助手。'},
        {'role': 'user', 'content': sys.argv[1]}
    ],
    'max_tokens': 10,
    'temperature': 0.1
}))" "$LONG_PROMPT" > payload.json

curl http://localhost:8000/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d @payload.json
```

使用 `watch -n 2 bash req.sh` 持續發送請求並觀察 LMCache 日誌輸出：

最後一比請求的日誌顯示 LMCache 有命中快取：

```txt
INFO 12-14 16:18:24 [async_llm.py:270] Added request chatcmpl-917d97645fb9403c8a73e31bb9135e42.
[2025-12-14 16:18:24,320] LMCache INFO: Reqid: chatcmpl-917d97645fb9403c8a73e31bb9135e42, Total tokens 497, LMCache hit tokens: 256, need to load: -240 (vllm_v1_adapter.py:1544:lmcache.integration.vllm.vllm_v1_adapter)
INFO:     127.0.0.1:36640 - "POST /v1/chat/completions HTTP/1.1" 200 OK
INFO 12-14 16:18:29 [loggers.py:118] Engine 000: Avg prompt throughput: 149.1 tokens/s, Avg generation throughput: 3.0 tokens/s, Running: 0 reqs, Waiting: 0 reqs, GPU KV cache usage: 0.0%, Prefix cache hit rate: 92.6%
```
