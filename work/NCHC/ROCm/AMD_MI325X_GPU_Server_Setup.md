# MI325X 8 GPU Server setup

今天我拿到了 8 張 MI325X 的伺服器，記錄一下怎麼安裝 ROCm

首先安裝好 Ubuntu 22.04 LTS 以後 ssh 進去更新一下套件

```shell
sudo apt update
sudo apt upgrade -y
```

## 安裝 dkms

再來先安裝 dkms

```shell
sudo apt install dkms build-essential linux-headers-$(uname -r)
```

dkms 裝好以後檢查狀態

```shell
dkms status
```

如果什麼輸出都沒有顯示就是正常

## 安裝 amdgpu-install

先檢查相容的 ROCm 和 driver 版本

![image](https://hackmd.io/_uploads/B1R-iduMbl.png)

有了 dkms 以後就可以裝 amdgpu-isntall，這個工具可以用來安裝 ROCm

```shell
wget https://repo.radeon.com/amdgpu-install/7.1.1/ubuntu/jammy/amdgpu-install_7.1.1.70101-1_all.deb
```

## 安裝 amdgpu-install

把剛剛用 wget 抓下來的 .deb 安裝包安裝

```shell
sudo apt install ./amdgpu-install_7.1.1.70101-1_all.deb
```

## 安裝 ROCm 工具鏈

使用 amdgpu-install 就可以快速安裝好 ROCm 的所有工具

```shell
sudo amdgpu-install
```

設定 ROCm 環境變數

```shell
echo 'export PATH=$PATH:/opt/rocm/bin' >> ~/.bashrc
source ~/.bashrc
```

到這邊應該就安裝完成，先重開機確保硬體正確載入。

```shell
sudo reboot now
```


使用 rocm-smi 測試 ROCm 安裝是否成功

```shell
rocm-smi
```
