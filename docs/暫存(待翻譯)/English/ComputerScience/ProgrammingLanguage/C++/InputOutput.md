---
tags: Note
---

# C++ Input Output

[TOC]

## Input
#### Example

```cpp=
int a;
cin >> a;
```

#### Explain

First line declare varible `a`  
Second line give a value to `a`  

## Output

#### Example

```cpp=
int a=1;
cout << "a=" << a;
```

#### Result

```
a=1
```

#### Explain

First line give `a` a value `1`  
Second line output `a=` varible value of `a`   

## All code

#### Example

```cpp=
#include <iostream>
using namespace std;
int main(){
    int a;
    cin >> a;
    cout << a;
    return 0;
}
```

#### Explain

初學 C\+\+ 時  
大部分的人會先給你這個格式  
以利後續快速教學  
第一行的 #include \<iostraem>  
是導入 C\+\+ 可以使用  
cin cout 的關鍵  
第二行的 using namespace std  
是讓整個程式的名稱空間設定在 standard  
同樣是為了後續快速教學而先這樣設定  
第三行的 int main\(\)\{  
代表的是程式的主要區塊開頭  
對應到第五行的大括號結尾  
第四行的 return 0 代表程式的結束  
程式會回傳0給系統  