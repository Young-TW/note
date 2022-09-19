---
tags: 筆記
---

# C# 筆記

[TOC]

### 參考資料

- [【C#】3小時初學者教學](https://youtu.be/T9BeejD3i0g)

## 開發環境

- VScode
- VS

### 專案結構

```
Csharp
├─bin
├─obj
├─.gitignore
├─Csharp.csproj
└─Program.cs
```

## 基本輸出輸入

### Hello world

- project.cs

```csharp=
using System;

namespace Csharp
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}

```

### user input

- project.cs

```csharp=
using System;

namespace Csharp
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}

```

## 資料型態



|  英文   |    中文    |    占用記憶體空間    |                         範圍                          |
|:-------:|:----------:|:--------------------:|:-----------------------------------------------------:|
|  short  |   短整數   |        2Byte         |                   -32,768 至 32,767                   |
|   int   |    整數    |        4Byte         |            -2,147,483,648 至2,147,483,647             |
|  long   |   長整數   |        8Byte         | -9,223,372,036,854,775,808至9,223,372,036,854,775,807 |
| ushort  | 無號短整數 |        2Byte         |                      0 至 65,535                      |
|  uint   |  無號整數  |        4Byte         |                  0 至 4,294,967,295                   |
|  ulong  | 無號長整數 |        8Byte         |            0 至 18,446,744,073,709,551,615            |
|  float  |   浮點數   |        4Byte         |                 1.5×10-45 至 3.4×1037                 |
| double  |  雙精準度  |        8Byte         |               5.0×10-324  至 1.7×10308                |
| decimal |    貨幣    |        16Byte        |                 1.0×10-28 至 7.9×1028                 |
|  char   |    字元    |        2Bytes        |                      0 到 65535                       |
| string  |    字串    |   依設定的字串長度而定   |                    1 到 231 個字元                    |

### string

## 資料結構 

### array

### 二微陣列

## 流程控制

### 判斷式

### if

### 迴圈

### for

### while

## class & object

## namespace & using

### method

### main

### constructor

## getter & setter

## 靜態

### static attribute 靜態屬性


### static method 靜態方法 & static class 靜態類別

## 繼承 inheritance