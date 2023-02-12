---
tags: 使用說明
---

# tmux

tmux 是一個用來讓終端機平行運作的工具  
tmux 可以實現多個終端機的切換  
非常適合用來管理server  

## 新增新的視窗

```shell=
tmux new -s "視窗名稱"
```

## 進入已開啟的視窗

```shell=
tmux a -t "視窗名稱"
```

## 水平分割視窗

`ctrl + b` -> `%`

## 垂直分割視窗

`ctrl + b` -> `"`

## 切換所在視窗

`ctrl + b` -> `O`

## 離開視窗

`ctrl + b` -> `d`