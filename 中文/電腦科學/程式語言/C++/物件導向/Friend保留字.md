---
tags: 筆記
---

# C++ Friend 保留字 (Friend keyword)

[TOC]

## 簡介

Friend 保留字允許一個 class 直接存取另一個 class 中 private 內的資料，
增加了物件互動的方便性，
但如果濫用 Friend 可能導致程式的不安全，
甚至失去了原本使用 private 的目的。  

## 語法

```cpp
class human{
    private:
        int age;
    public:
        string name;
        friend class cat;
};

class cat{
    private:
        int weight;
        int age;
    public:
        string name;
};
```



<!-- 未完成 -->