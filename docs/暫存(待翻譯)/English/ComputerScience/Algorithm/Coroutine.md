---
tags: Note
---

# Coroutine

## 參考資料

- https://www.maxlist.xyz/2020/03/29/python-coroutine/

## Introduction

協程的功能可以把工作的時間切片  
讓多個功能達到類似同時執行的感覺  
但其實是輪流用一小段時間跑  

## asyncio library

asyncio 函式庫常用於協程  

## await & async Syntactic Sugar

### await

用來標記 Coroutine 切換暫停和繼續的點  

### async

用來宣告 function 能夠有異步的功能  