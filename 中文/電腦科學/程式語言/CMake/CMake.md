---
tags: Note
---

# CMake

[TOC]

## 參考

- [維基百科](https://zh.wikibooks.org/zh-tw/CMake_%E5%85%A5%E9%96%80/%E5%9F%BA%E6%9C%AC%E8%AA%9E%E6%B3%95)

## 簡介

CMake 是一個用於跨平臺自動化開發環境的編譯等工作的工具，
這讓編譯 C++ 專案變得簡潔許多。

## 使用方法

常見的寫法是會設定好 CMake 最低版本要求，
並且寫好專案名稱和版本，
接著設定 C++ 版本，
再選擇要產生的執行檔從哪些原始碼生成。

以下會提供一個 `CMakeLists.txt` 範例

### 基本用法

```cmake
cmake_minimum_required(VERSION 3.0.0)
project(my_app VERSION 0.0.0)

set(CMAKE_CXX_STANDARD 23)

add_executable(${PROJECT_NAME} ./main.cpp)
```

首先要讓 CMake 產生 Makefile，可以使用以下指令：

```bash
cmake . -B build
```

如果有更動 CMakeLists.txt 檔案或是原始碼，可以重新輸入上面的指令產生新的 Makefile。

擁有 Makefile 之後就可以使用以下指令進行編譯：

```bash
cmake --build build
```

編譯完成後可執行檔會在 `build` 目錄中。
依照範例的設定，執行檔名稱會是 `my_app`。
輸入指令執行剛剛編譯的可執行檔：

```bash
./build/my_app
```

### 安裝目標專案

如果想要使用 cmake 安裝開發好的程式可以使用下面的範例：

```cmake
cmake_minimum_required(VERSION 3.0.0)
project(my_app VERSION 0.0.0)

set(CMAKE_CXX_STANDARD 23)

add_executable(${PROJECT_NAME} ./main.cpp)

install(TARGETS ${PROJECT_NAME})
```

接下來只要在專案目錄中使用指令就能直接安裝：

```bash
cmake --build build --config RELEASE
cmake --install build
```

<!-- 未完成 -->