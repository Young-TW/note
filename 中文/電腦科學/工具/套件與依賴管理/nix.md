# Nix

Nix 是一個宣告式的套件管理工具，主要用於 Linux 和其他 Unix-like 系統。它允許用戶定義和管理軟體包的安裝、配置和依賴關係，並提供了一個可靠的方式來構建和部署應用程式。

## Nix 與 NixOS

Nix 是一個獨立的套件管理系統，而 NixOS 是基於 Nix 的 Linux 發行版。NixOS 使用 Nix 作為其主要的套件管理工具，並提供了一個完整的系統配置管理功能。

## Nix 基礎用法

以下先示範在 NixOS 中使用 Nix 的基本操作：

首先，你擁有一個設定檔位於 `/etc/nixos/configuration.nix`，這是 NixOS 的主要配置檔案。你可以在這個檔案中定義系統的套件、服務和其他配置。

使用 Nix 時(不含 flakes)，你需要使用預設的 `nano` 編輯器修改這個檔案

```bash
sudo nano /etc/nixos/configuration.nix
```

並且找到 `environment.systemPackages = with pkgs; [];` 並把你想要安裝的套件添加到這個列表中。例如，如果你想要安裝 `htop` 和 `git`，你可以這樣修改：

```nix
environment.systemPackages = with pkgs; [
  htop
  git
];

然後執行以下命令來應用更改：

```bash
sudo nixos-rebuild switch
```

這行命令會依照 `/etc/nixos/configuration.nix` 重新構建 NixOS 系統，並應用你在配置檔案中所做的更改。

這就是 NixOS 最基本的使用方式。Nix 也可以在其他 Linux 發行版甚至 macOS 上使用，但通常需要額外的配置。
