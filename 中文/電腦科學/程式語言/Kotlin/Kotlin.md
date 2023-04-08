---
tags: 筆記
---

# Kotlin

## 變數型式

![](https://i.imgur.com/E4OU161.png)

### 變數定義

```kotlin=
/*var可變*/
/*val不可變*/
val a: Int = 1//預設型式
val b = 1//自動判斷
val c: Int//只定義變數則需給予型式
```

### 支援:

* 十進位
* 二進位 (0b開頭)
* 十六進位 (0x開頭)
* 長整型 (L結尾)
* 不支持八進位

----

## Basic Rule

### Package

`package com.example` 定義package
默認就會引入基本的package了。

### Function

#### Basic

```kotlin=
fun example(變數: 型式): 回傳型式 {/*注意 回傳型式第一個字元大寫*/
    return 回傳的東西
}
```

也可以使用單行函數

```kotlin=
fun example(變數a: 型式, 變數b: 型式) = 要回傳的東西
```

但是 如果是public的函數 除了無回傳值的函數外
<strong>都需要將回傳型式標示出來</strong>

#### 可變數量的參數:

<strong>varargs</strong>為可變數量參數之定義型式

Ex:

```kotlin=
fun vars(vararg v:Int){
    for(vt in v){
        print(vt)
    }
}

fun main(args: Array<String>) {
    vars(1,2,3,4,5)  // 輸出12345
}
```

#### 中綴表示法:

標有<strong>infix</strong>的函數可使用中綴表示法
但是定義前有限制:
* 必須是成員函數或是擴展函數(一般的函數跟一般函數的擴展)
* 必須只有一個參數
* 其參數不可是`varargs`且無默認值
用法:

```kotlin=
infix fun add(s: String) {
/*owo*/
}
fun main(){
    this add "a"
    add("a")
}
```

須注意的是 他的層級低於一般的運算式

Ex:

```kotlin=
infix fun sh1(a: Int, b: Int): Int {
    return a + b
}
fun main(){
    1 sh1 2 + 3 //1 + (2 + 3)
}
```

#### 泛式函數:

```kotlin=
fun <T> singletonList(item: T): List<T> { /*……*/ }
```

#### Lambda匿名函數:

```kotlin=
fun main(args: Array<String>) {
    val sumLambda: (Int, Int) -> Int = {x,y -> x+y}
    println(sumLambda(1,2))  // 輸出 3
}
```

### Other

#### Null檢查

```kotlin=
var age: String? = "23"
val ages = age!!.toInt()
//不做處理返回 null
val ages1 = age?.toInt()
//age為空返回-1
val ages2 = age?.toInt() ?: -1
```

#### 類型檢測:

利用is運算子確認Any的型式 如果不是 則將其轉換