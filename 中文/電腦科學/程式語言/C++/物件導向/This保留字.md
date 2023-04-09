---
tags: 筆記
---

# C++ This 保留字 (This keyword)

[TOC]

## 簡介

This 關鍵字常在運算子多載中使用到，
功能為指向物件本身，
也就是一個指標。

以下會示範 This 的用法。

## 語法

```cpp
class Stack {
    public:
        vector<int> v_stack;

    operator+(Stack &obj) {
        Stack res;
        for (int i=0; i<this->size; i++) {
            res.add(this->stack.at(i));
        }
        for (int i=0; i<obj.size; i++) {
            res.add(obj.stack.at(i));
        }
        return res;
    }
}

int main() {
    Stack a;
    Stack b;
    a = a+b;
}
```

原本的物件是沒有辦法直接相加的，
不過只要做運算子多載就能夠讓物件互相做許多不同的運算，
上面這段範例程式碼使用到 this 指標就是在運算子多載，
但是僅有這幾行不足以執行，
因為裡面還有調用到其他函式，
但從這段程式碼明顯可以看出 this 的功能，
用簡單一句話來說就是 this-> 底下的東西就是在物件本身內。

<!-- 未完成 -->