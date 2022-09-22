---
tags: Note
---

# Web Frontend Note

[TOC]

## HTML (超文本標記語言)

### 文件結構:

```htmlembedded=
<!DOCTYPE html>
<html>
  <head>
    <title>Page Title</title>
  </head>
  <body>
    <h1>This is a Heading</h1>
    <p>This is a paragraph.</p>
  </body>
</html>
```

以層狀標籤配合縮排來框住裡面的內容  

### Head
#### Introduction
head通常拿來放一歇頁面看不到的內容  
像是連結到哪個CSS檔案  
還有字元編碼  

#### 標籤表

| 語法 |  描述  |
|:---:|:---:|
|title|標題|
|meta|字元編碼|
|link|連結|

### Body
#### 簡介
body的內容就是頁面上顯示出的畫面  
經過這些標籤的排版之後呈現出來的樣子就是網頁  

#### 標籤表

| 語法 |  描述  |
|:---:|:---:|
|p|段落|
|h1~h6|標題|
|div|區域|
|hr|換行|
|a|連結|
|image|圖片|
|video|影片|
|li|列表(每項)|
|ul|列表(整體)|

## CSS (階層式樣式表)
### 文件結構:
```css=
body{
  color: #000000;
  margin: auto;
  width: 100%;
}
```
### 標籤:

| 語法 |  描述  |
|:---:|:---:|
|color|字體顏色|
|background-color|背景顏色|
|background-image|背景圖片|
|margin|邊距|
|width|寬度|
|height|高度|
|float|移動位置|

### 選擇器
CSS可以配合HTML元素的``id`` ``class`` ``tag``來選取標籤  
#### 範例
##### HTML:
```htmlembedded=
<h1 id='title'>
title
</h1>
```
##### CSS:
```css=
.title{
  color: blue;
  width: 100%;
}
```
#### 結果
<h1 style=
"color='blue'
 width='100%'">
  title
</h1>

## [JavaScript Note](https://hackmd.io/@Young-/H1HWv5Wqu)
