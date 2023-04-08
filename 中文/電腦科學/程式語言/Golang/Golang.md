---
tags: 筆記
---

# Golang 筆記

[TOC]

# 基礎

## 簡介

Golang 是一個由 Google 開發以及維護的開源程式語言
執行速度非常快且輕量化
也被稱為21世紀的 C 語言

## 資源

- [鐵人賽1211](https://ithelp.ithome.com.tw/users/20103452/ironman/1211)
- [鐵人賽1947](https://ithelp.ithome.com.tw/users/20103651/ironman/1947)
- [鐵人賽2616](https://ithelp.ithome.com.tw/users/20120698/ironman/2616)
- [鐵人賽3155](https://ithelp.ithome.com.tw/users/20125192/ironman/3155)

## 環境建置

[下載安裝檔](https://golang.org/dl/)

## Hello World

```go=
package main

import "fmt"

func main() {
    fmt.Println("Hello World!")
}
```

## 輸入輸出

```go=
func main() {
    var a int
    fmt.Scanln(&a)
    fmt.Println(a)
}
```

## Package

[常用基本庫介紹](https://ithelp.ithome.com.tw/articles/10223934)

[Go Module 與 Go get 說明](https://hoohoo.top/blog/go-module-and-go-get-common-parameter-descriptions/)

### main

### fmt

用來提供基本輸入輸出的包
如果要在終端機與程式互動幾乎都會用到它

### strings

### time

顧名思義就是時間相關的函式

# 宣告

Golang 的宣告會把資料型態寫在變數名稱的後面
並且以 var 為關鍵字進行宣告

```go=
var Young int = 1
```

## 變數與常數

### 變數

變數在宣告後可以改變其值

```go=
import "fmt"

var hello = 123
hello = 4
fmt.Println(hello)
```

結果：

```
4
```

### 常數

常數在宣告後就無法改變其值
通常習慣宣告常數名稱會全大寫

```go=
const HELLO = 123
```

## 資料型態

介紹不同的資料型態
需要注意的是 在 go 的程式內
不同的資料型態不能直接進行運算

### int

int 用於宣告整數

- int8
    - range: -128~127
- int16
    - range: -32768~32767
- int32
- int64

### float

float 指的是浮點數
也就是小數

- float32
- float64

## 資料結構

### struct 結構體

可以把多個變數存在同一個結構體內

```go=
package main

import "fmt"

type st struct {
	Young string
	Zanzan string
	xigua int
}

func main() {
	var st1 = st{
		Young: "我是Young 我不會寫程式",
		Zanzan: "西瓜好虐",
		xigua: 7,
	}
	fmt.Println(st1)
	fmt.Println(st1.Zanzan)
}
```

#### Nested Structure

### array

```go=
package main

import "fmt"

func main() {
	fmt.Println("hello")
	var a [30]int
	a[2] = 2
	fmt.Println(a)
	for i := 0; i < len(a); i++ {
		a[i] = i
	}
	fmt.Println(a)
}
```

### slice

### map

# 運算子

# 流程控制

## 判斷式


```go=
package main

import "fmt"

func main() {

}
```

## 迴圈

golang 本身只有 for 迴圈
但是用 for 迴圈就足以做到所有事情

### 無限迴圈

```go=
package main

import "fmt"

func main() {
    for {
        fmt.Println("hello")
    }
}
```

### in range

```go=
package main

import "fmt"

func main() {
    for var i=0; i<5; i++ {
        fmt.Println("hello")
    }
}
```

### while

```go=
package main

import "fmt"

func main() {
    var i int = 0
    for i<5 {
        fmt.Println("hello")
        i++
    }
}
```

## 函式

### 無回傳值

```go=
package main

import "fmt"

func Young(){
    fmt.Println("Hello Young!")
}

func main() {
    Young()
}
```

### 一個回傳值

```go=
package main

import "fmt"

func main() {

}
```

### 多個回傳值

```go=
package main

import "fmt"

func main() {

}
```

# 實作

## 最大公因數 (gcd)

```go=
package main

import "fmt"

func smaller(a,b int) int {
	if a>b {
		return b
	} else {
		return a
	}
}

func gcd(a, b int) int {
	var c int = smaller(a,b)

	for i := c; i > 1; i-- {
		if a%i == 0 && b%i == 0 {
			return i
		}
	}

	return 1
}

func main() {
	var a, b int

	fmt.Println("gcd: please input two int. ")
	_, _ = fmt.Scanf("%d %d", &a, &b)

	fmt.Println(gcd(a, b))
}
```