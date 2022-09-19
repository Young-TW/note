---
tags: Note
---

# C++ Loop

[TOC]

## For Loop

### Basic For Loop

```cpp
for(int i=0;i<10;i++){
    
}
```

### Auto(vector)

```cpp
vector<int> n;
for(auto i : n){
    
}
```

### Unlimited Loop

```cpp
for(;;){

}
```

## While Loop

### Usage

當條件成立時
```cpp
while(/*條件*/){

}
```

### Unlimited Loop

```cpp
while(1){

}

// or

while(True){

}
```

以下為以前的舊筆記  

## 迴圈
### for
#### 基本語法
```cpp=
for (變數=初始值;變數<結束值;變數++){
    動作;
}
```
#### 範例
```cpp=
for (i=1;i<3;i++){
    cout << i;
}
```
#### 結果
```
12
```
#### 結論
第一圈會用初始值運行  
第二圈因為``i++``所以會印出``2``  
第三圈因為``i<3``不成立所以結束迴圈  
### while
#### 基本語法
```cpp=
while (條件){
    動作;
}
```
#### 範例
```cpp=
int a=1;
while (a<3){
    cout << a;
    a++;
}
```
#### 結果
```
12
```
#### 結論
一開始給定a初始值1  
第一圈印出1之後a+1  
第二圈印出2再a+1  
第三圈a<3不成立所以結束迴圈  
while用中文表示就是  
當...成立時執行  
條件判斷的結果以布林值表示  
所以  
```cpp=
while (1){  
}  
```
就是無限迴圈  
### 特例
- break:
跳脫迴圈
- continue:
直接從下一圈開頭繼續