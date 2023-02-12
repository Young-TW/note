---
image: https://i.imgur.com/vupSN9u.png
description: Python 筆記
tags: 筆記
---

# Python 筆記

[TOC]

## 簡介
Python是一種直譯式的程式語言  
Python和大多數其他語言比起來  
算是高階的程式語言  

## 功能
Python的功能有很多  

- 數學 
- 深度學習 
- 網路爬蟲
- 網頁後端
- APP與遊戲開發
- 資料處理
- Discord Bot

因大多數底層知識都已經被整理好  
並且語法較為接近人類  
所以Python適合新手學習  

## 資料型態與結構
### 資料型態
Python的資料型態種類如下  

| 英文  |  中文  |
|:-----:|:------:|
|  int  |  整數  |
| float | 浮點數 |
| bool  | 布林值 |
|  chr  |  字元  |

在Python中的變數不需要宣告  
並且變數會自動指定資料形態  
當要建立一個變數時  
直接給定變數一個值  
int(整數)和數學的整數定一一樣  
float(浮點數)小數點後有還有非``0``的數  
bool(布林值)是或否 也就是``1``或``0``  
chr(字元)可以存一個字  
### 資料型態的轉換
#### 範例
```python=
a=1
print(type(a))
a=str(a)
print(type(a))
```
#### 結果
```
<class 'int'>  
<class 'str'>
```
#### 結論
第一次直接給定初始值``a=1``  
接著自動給定變數``a``資料形態``int``  
所以第一次 print 變數``a``的type時印出  
``<class 'int'>``  
第二次將a的資料形態轉為 str  
再次print(type(a))  
印出的是已經轉換的資料形態  
``<class 'str'>``  
### 資料結構
Python的資料結構種類如下  

| 英文  |  中文  |
|:-----:|:------:|
| list  |  串列  |
| tuple |  元組  |
| dict  |  字典  |
|  str  |  字串  |

dict是Dictionary(字典)的縮寫  
str是string(字串)的縮寫  
list就像其他語言裡的array(陣列)很像  
給定一個名稱就可以存多筆資料在裡面  
tuple的概念是 不能改變數值的list  
使用方法相同 但是tuple給定數值後就不能更改  
dict是值鍵對(key-value-pair)  
可以理解成鑰匙和鎖頭  
每一組都是一個鍵對上一個值  
str可以理解成儲存字元的list  
## 基本語法
### import
#### 語法
```python=
import 套件
from 套件 import 功能
import 套件 as 新名稱
from 套件 import *
```
#### 範例
```python=
import os
from os import system
import os as myos
from os import *
```
#### 解說
1. 普通的import
2. 從指定的套件下import單個功能
3. import後更改套件名稱
4. 從指定的套件下import全部的功能

使用 `from import` 的好處是可以直接調用函式  
不需要先加入套件名稱  
### input
#### 語法
```python=
變數 = input()
```
#### 範例
```python=
a = input()
```
#### 解說
將輸入值指定到變數``a``  
``a``的資料型態會交由Python自動分配  
### print
#### 語法
```python=
print("內容")
print(變數)
```
#### 範例
```python=
a=1
print("Hello world!")
print(a)
print(f"Hello world{a}")
```
#### 結果
```
Hello world!
1 
Hello world1
```  
#### 解說
第一行印出字串``Hello world!``  
第二行印數變數``a``  
第三行印出格式化字串``Hello world1``  
## 判斷式
和其他語言一樣  
但Python使用縮牌判定區塊  
### if
#### 語法
```python=
if 條件:
    執行動作
```
#### 範例
```python=
a=1
if a==1:
    print("a=1")
```
#### 結果
```
a=1
```
#### 結論
如果條件成立  
會執行判斷式內的動作  
### else
#### 語法
```python=
if 條件:
    執行動作
else:
    執行動作
```
#### 範例
```python=
a=2
if a==1:
    print("a=1")
else:
    print("a!=1")
```
#### 結果
```
a!=1
```
#### 結論
如果第一個條件不成立  
就會執行else的動作  
### else if
#### 語法
```python=
if 條件:
    執行動作
elif 條件:
    執行動作
```
#### 範例
```python=
a=4
if a==1:
    print("a=1")
elif a>3:
    print("a>3")
```
#### 結果
```
a>3
```
#### 結論
如果第一個條件成立  
就不會執行elif的判斷  
反之 如果第一個條件不成立  
就會執行elif的判斷  
## 迴圈
### for i in n
#### 語法
```python=
串列=[1,2,3,4]
for 變數 in 串列:
    print(串列的第(變數)項)
```
#### 範例
```python=
n=[1,2,3,4]
for i in n:
    print(i)
```
#### 結果
```
1
2
3 
4
```
#### 結論
這個迴圈第一圈時``i=n[0]``  
所以印出``1``  
在來第二圈``i=n[1]``  
以此類推  
### for i in range(x):
#### 語法
```python=
for 變數 in range(值):
    動作
```
#### 範例
```python=
for a in range(5):
    print(a)
```
#### 結果
```
0
1
2 
3
4
```  
#### 結論
Python的for ``a`` in range(``b``):  
意思是總共跑``b``圈  
目前在第``a+1``圈  
因為Python的特性  
``a``是從``0``開始算  
### while
#### 語法
```python=
while 條件:
    動作
```
#### 範例
```python=
a=1
while a<3:
    a=a+1
```
#### 結果
```
1
2
```
#### 結論
一開始給定``a``初始值``1``  
第一圈印出``1``之後``a+1``  
第二圈印出``2``再``a+1``  
第三圈``a<3``不成立所以結束迴圈  
while用中文表示就是  
當...成立時執行  
條件判斷的結果以布林值表示  
所以while ``1``:  
就是無限迴圈  
### 特例
- break:
跳脫迴圈
- continue:
直接從下一圈開頭繼續
## 函式
#### 語法
```python=
def 函式名稱(傳入值):
    動作
```
#### 範例
```python=
n=input()
n=int(n)
def double(n):
    n=2*n
    return n
print(double(n))
```
#### 結果
輸入  
```
3
```
輸出  
```
6
```
#### 結論
第一行要求輸入數字``n``  
第二行將``n``的資料型態轉換為``int``  
三至五行定義函式``double``  
將傳入值乘``2``後回傳  

使用函式可以實現結構化程式設計  
對於程式debug有很大幫助  
每個函式都只做自己的工作  
分界明顯較不容易出錯  
### 遞迴
#### 語法
```python=
def 函式名稱(傳入值):
    動作
    函式名稱(傳入值) #呼叫自己
```
#### 範例
```python=
import os
n=input('input ')
n=int(n)
a=1
def fact(n):
    if n == 0:
        return 1
    else:
        global a
        a=a*n
        return fact(n-1)
fact(n)
print(a)
os.system('pause')
```
#### 結果
輸入
```
5
```
輸出
```
120
```
#### 結論
使用遞迴解決數學的階乘  
比起迴圈執行速度更有效率  


# Python Discord bot

Python 可以用來撰寫 Discord bot  
以下會提供範例  

## 基本 Python Discord bot

```python=
import discord
from discord.ext import commands,tasks

intents = discord.Intents.all()
bot=commands.Bot(command_prefix=".",intents=intents)

@bot.event
async def on_ready():
    print('We have logged in as {0.user}'.format(bot))

@bot.command()
async def ping(ctx):
    await ctx.send(f'{round(bot.latency*1000)}ms')

bot.run('TOKEN')
```

## 協程

## 指令的撰寫