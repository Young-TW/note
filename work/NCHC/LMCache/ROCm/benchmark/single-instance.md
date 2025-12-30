# Singel vLLM Instance Benchmark

因為 vLLM 單節點的模型推論透過 Prefix Cache 已經可以在 GPU 之間透過 P2P 傳輸 KV Cache（全部 GPU 一起做 Prefill/Decode）, 所以先不使用 LMCache 來做硬體上的 PD 分離。

這邊的 benchmark 主要是測試單一實例下，vLLM Prefix Cache 對於多次請求的加速效果。

如果將來需要擴充到多節點，則可以再啟用 LMCache 來做跨節點的 KV Cache 傳輸。

以下皆使用 `Llama-3.1-70B-Instruct` (FP16) 模型進行測試。

## 啟動 Docker Container

使用 `sudo docker compose up -d` 啟動 vLLM 伺服器：

```yaml
services:
  vllm:
    # 注意：請確認使用支援 ROCm 的映像檔標籤
    # 官方通常會提供如 vllm/vllm-openai:latest-rocm 的標籤
    # 或是使用 AMD Infinity Hub 提供的映像檔
    # image: vllm/vllm-openai:latest-rocm
    image: rocm/vllm-dev:nightly
    container_name: vllm-server
    restart: always

    # === AMD ROCm 關鍵硬體設定 ===
    devices:
      - /dev/kfd:/dev/kfd
      - /dev/dri:/dev/dri

    # === 記憶體與通訊優化 ===
    # TP=8 非常吃 Shared Memory，務必開啟 ipc: host
    ipc: host
    # 某些 ROCm 版本需要 video 群組權限
    group_add:
      - video
    # MI300X 有時需要較高的系統權限來存取硬體計數器或特定驅動功能
    cap_add:
      - SYS_PTRACE
    security_opt:
      - seccomp:unconfined

    # === 儲存卷掛載 ===
    volumes:
      # 1. 掛載模型權重 (Host路徑 : Container內路徑)
      - /home/young/models/Llama-3.1-70B-Instruct:/app/model
      # 2. (選用) 掛載 HuggingFace Cache，避免重複下載
      - ~/.cache/huggingface:/root/.cache/huggingface

    # === 環境變數 ===
    environment:
      # - HUGGING_FACE_HUB_TOKEN=
      # 若遇到 RCCL P2P 初始化問題，可嘗試取消註解下面這行
      # - NCCL_P2P_DISABLE=0
      # 針對 MI300X 建議的 RCCL 通道優化 (視情況調整)
      - NCCL_MIN_NCHANNELS=112

    ports:
      - "8000:8000"

    # === 啟動指令 ===
    # 注意：這裡的 --model 路徑必須對應到上面的 volumes container 路徑 (/app/model)
    command: >
      python3 -m vllm.entrypoints.openai.api_server
      --model /app/model
      --tensor-parallel-size 8
      --enable-prefix-caching
      --enable-chunked-prefill
      --max-num-batched-tokens 2048
      --port 8000
      --gpu-memory-utilization 0.90
```

## Benchmark 測試

測試的 Python 腳本較長就先不放在這，下面四個參數可以依照情境調整：

```py
# Benchmark settings
CONCURRENCY = 128           # Max simultaneous in-flight requests
TOTAL_REQUESTS = 500        # Total requests to perform
INPUT_LEN_APPROX = 2048     # Target input token length
MAX_TOKENS = 512            # Max output tokens
```

測試結果如圖：

![result](./result.png)

左上角為首 Token 延遲，絕大部分請求都穩定在 0.3s 以內，整體呈長尾分布，p99 達到 2.52s。

右上角為 Decode 吞吐量，平均在 24.2 Token/s。

下面這張圖顯示了請求發出到完成的總時長和輸出長度分佈，模型輸出速度幾乎保持一致。
