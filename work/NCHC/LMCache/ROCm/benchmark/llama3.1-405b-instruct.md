# Llama3.1-405B-Instruct ROCm 環境基準測試

先下載模型，設定好環境變數 `$HF_TOKEN` 後，執行以下指令：

```bash
python3 -c "import os; from huggingface_hub import snapshot_download; snapshot_download(repo_id='meta-llama/Llama-3.1-405B-Instruct', local_dir=os.path.expanduser('~/models/Llama-3.1-405B-Instruct'), local_dir_use_symlinks=False)"

```

