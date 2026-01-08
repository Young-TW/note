# 透過 vLLM 在 ROCm 環境下實現 PD 分離

## Prefill

Prefill 節點的啟動命令：

```sh
vllm.entrypoints.api_server \
    --model Qwen/Qwen2-7B-Instruct \
    --port 8001 \
    --kv-role producer \
    --dtype bfloat16 \
    --tensor-parallel-size 4
```

| 參數                   | 說明                | 範例值                 | 備註                            |
| ---------------------- | ------------------- | ---------------------- | ------------------------------- |
| --model                | 要載入的模型名稱    | Qwen/Qwen2-7B-Instruct |                                 |
| --port                 | 服務監聽的 TCP 埠號 | 8001                   | Decode 節點將連接此埠號         |
| --kv-role              | 設定該服務的角色    | producer               | 必須設定為 producer             |
| --dtype                | 模型使用的精度      | bfloat16               | 依照您的 AMD GPU 支援和需求調整 |
| --tensor-parallel-size | 使用的 GPU 數量     | 4                      | 適用於單一節點上的多張 AMD GPU  |

## Decode

Decode(KV Consumer) 節點的啟動命令：

```sh
vllm.entrypoints.api_server \
    --model Qwen/Qwen2-7B-Instruct \
    --port 8002 \
    --kv-role consumer \
    --producer-url http://192.168.1.100:8001 \
    --dtype bfloat16 \
    --max-model-len 8192 \
    --tensor-parallel-size 4
```

| 參數                   | 說明                       | 範例值                    | 備註                            |
| ---------------------- | -------------------------- | ------------------------- | ------------------------------- |
| --model                | 要載入的模型名稱           | Qwen/Qwen2-7B-Instruct    | 必須與 Prefill 節點的模型相同   |
| --port                 | 服務監聽的 TCP 埠號        | 8002                      | 這是外部用戶實際呼叫的埠號      |
| --kv-role              | 設定該服務的角色           | consumer                  | 必須設定為 consumer             |
| --producer-url         | Prefill 節點的位址         | http://192.168.1.100:8001 | 替換為 Prefill 服務的 IP 和埠號 |
| --max-model-len        | 模型能處理的最大上下文長度 | 8192                      | 決定了 KV Cache 的最大大小      |
| --tensor-parallel-size | 使用的 GPU 數量            | 4                         | 必須與 Prefill 節點的設定匹配   |
