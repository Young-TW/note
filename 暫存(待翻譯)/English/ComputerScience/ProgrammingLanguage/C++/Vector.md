---
tags: Note
---

# C++ Vector

[TOC]

## Introduction

向量屬於 C++ 標準模板庫的其中一種資料容器  
因為大小能夠重新配置等因素  
可以用來取代 Array 的不足  
但也有其缺點所在  

## Basic Usage
#### Syntax

```cpp
vector<int> v(3);
```

This line declare 3 int space:  

`vector[0], vector[1], vector[2]`  

#### Example

```cpp
vector<int> v(3);
for(auto i : v){
    i = 1;
}
for(auto i : v){
    cout << i << " ";
}
```

#### Result

`1 1 1`

#### Explain

向量的使用和陣列非常相近  
所以上面範例看起來會很接近陣列  
但接下來的操作就是向量的不可取代之處了  

## Advance

### push_back()
### erase()