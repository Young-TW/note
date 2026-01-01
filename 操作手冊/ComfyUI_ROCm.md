# ComfyUI ROCm 安裝

## 啟動 Docker ROCm 容器（不包含 ComfyUI）

```bash
podman run -it --name rocm7 \
  --device /dev/kfd \
  --device /dev/dri \
  --security-opt=label=disable \
  docker.io/rocm/dev-ubuntu-24.04:latest \
  /bin/bash
```

## 安裝 ComfyUI

### Clone ComfyUI 原始碼

```bash
apt update
apt install git
git clone https://github.com/comfyanonymous/ComfyUI.git
cd ComfyUI
```

### 安裝 Python 套件

先開 venv

```bash
apt install python3.12-venv
python3 -m venv venv
source venv/bin/activate
```

安裝 ROCm 版本的 PyTorch 和相關套件

```bash
# 先升級 pip 以防萬一
pip install --upgrade pip

pip install --pre torch torchvision torchaudio --index-url https://download.pytorch.org/whl/nightly/rocm7.1
```

安裝 ComfyUI 依賴

```bash
pip install -r requirements.txt
```

### 設定環境變數

```bash
# for RDNA 4
export HSA_OVERRIDE_GFX_VERSION=12.0.1
```

```bash
# 減少碎形記憶體，避免長時間跑圖 OOM
export PYTORCH_HIP_ALLOC_CONF=garbage_collection_threshold:0.8,max_split_size_mb:512
```

### 啟動 ComfyUI

```bash
python main.py --listen 0.0.0.0 --port 8188
```

### 依照掛載的目錄設定 ComfyUI 的模型路徑

```bash
# 1. 確保在正確目錄
cd /root/ComfyUI

# 2. 用 echo 直接寫入正確的設定 (包含 Z-Image 修正)
echo 'comfyui:
    base_path: /app/storage
    is_default: false
    checkpoints: models/checkpoints
    clip: models/clip
    clip_vision: models/clip_vision
    configs: models/configs
    controlnet: models/controlnet
    embeddings: models/embeddings
    loras: models/loras
    upscale_models: models/upscale_models
    vae: models/vae
    unet: models/unet
    diffusion_models: models/unet' > extra_model_paths.yaml
```
