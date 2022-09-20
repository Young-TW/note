---
tags: Note
---

# C++ Flow Control

[TOC]

## If
#### Syntax

```cpp=
if (/*condition*/){
    /*action*/;
}
```

#### Example

```cpp=
int a=1;
if (a==1){
    cout << "a=1";
}
```

#### Result

```
a=1
```

#### 結論
若條件成立則執行動作  
條件不成利則不執行  
### else
#### Syntax
```cpp=
if (/*condition*/){
    /*action*/;
}
else{
    /*action*/;
}
```
#### Example
```cpp=
int a=1
if (a!=1){
    cout << "a!=1";
}
else{
    cout << "a=1";
}
```
#### Result

```
a=1
```

#### Conclusion

若if條件未成立  
則執行else內的動作  

### else if

#### Syntax

```cpp=
if (條件){
    動作
}
else if (條件){
    動作
}
```

#### Example

```cpp=
int a=1
if (a!=1){
    cout << "a!=1";
}
else if (a<3){
    cout << "a<3";
}
```

#### Result

```
a<3
```

#### Conclusion

若第一次的條件不成立  
則執行else if的判斷  

## Switch case

switch case 的概念  
可以用多個 else if 來想像  

#### Syntax

```cpp=
switch (輸入值){
    case 選項:
        動作;
    case 選項:
        動作;
    case 選項:
        動作;
}
```

#### Example

```cpp=
let a=1;
switch (a){
    case 1:
        cout << "a=1";
        break;
    case 2:
        cout << "a=2";
        break;
    case 3:
        cout << "a=3";
        break;
}
```

#### Result

```
a=2
```

#### Conclusion

When `input value` = `選項`  
執行該`選項`內的`動作`  
需要注意的是  
case 內的動作結束後要加上 break;  
不然下面的每個 case 都會被執行一次  