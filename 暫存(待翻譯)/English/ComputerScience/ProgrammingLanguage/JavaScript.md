# JavaScript 筆記
###### tags: `筆記`

## 編輯器
使用 vs code 中的 live server 擴充套件  
新增一資料夾  
在資料夾底下建立 `index.html`  
並將以下的 html 複製進 `index.html`  
```htmlembedded=
<!DOCTYPE html> 
<html>
<head>
<meta charset="UTF-8">
<title>title</title>
</head>

<body>
<script src='./script.js'></script>
</body>
</html>
```
在同一資料夾下建立 `script.js`  
接下來的 javascript 都會寫在這個 `script.js` 內  

## 宣告
- let

建立可更改其值的變數  
```javascript=
let a = 1;
```

- var

建立可更改其值的變數  
```javascript=
var b = 1;
```

- const

建立不可更改其值的變數  
```javascript=
const c = 1;
```
javascript 的宣告不需要指定資料型態  
let 和 var 的差異
### 資料型態
javascript 的資料型態如下

### 資料結構
- array

建立陣列  
```javascript=
let array = [1,2,3,4]
```
- object

建立物件  
```javascript=
let object = {a:1,b:2}
```
## 運算子
### 邏輯運算子
- ===

判斷是否相等
- !==

判斷是否不相等
### 數學運算子
- \+

相加
- \-

相減
- \*

相乘
- /

相除
- %

取餘數
- =

將等號右側的值放進等號左側
## 輸入輸出
### concole.log
#### 基本語法
```javascript=
console.log(內容);
```
#### 範例
```javascript=
console.log("hello");
```
#### 結果
```
hello
```
#### 結論
console 指的是主控台  
log 指的是日誌  
console.log 指的是主控台的日誌  
也就是在瀏覽器內按下 F12  
選擇 console 可以看到的內容  
## 判斷式
### if
#### 基本語法
```javascript=
if (條件) {
    動作;
}
```
#### 範例
```javascript=
let a=1;
if (a===1) {
    console.log("a=1");
}
```
#### 結果
```
a=1
```
#### 結論
當條件成立時  
執行大括弧內的程式  
### else
#### 基本語法
```javascript=
if (條件) {
    動作;
}
else {
    動作;
}
```
#### 範例
```javascript=
var a=2;
if (a===1) {
    console.log("a=1");
}
else {
    console.log("a!=1");
}
```
#### 結果
```
a!=1
```
#### 結論
當 if 的條件不成立時  
執行 else 大括弧內的程式  
### else if
#### 基本語法
```javascript=
if (條件) {
    動作;
}
else if (條件) {
    動作;
}
else {
    動作;
}
```

#### 範例
```javascript=
var a=2;
if (a===1) {
    console.log("a=1");
}
else if (a===2){
    console.log("a=2");
}
else {
    console.log("a!=1 or 2")
}
```
#### 結果
```
a=2
```
#### 結論
當第一個條件不成立時  
才會執行第五行 else if 的判斷  
當
### switch case
switch case 的概念  
可以用多個 else if 來想像  
#### 基本語法
```javascript=
switch (輸入值){
    case 選項:
        動作;
    case 選項:
        動作;
    case 選項:
        動作;
}
```
#### 範例
```javascript=
let a=1;
switch (a){
    case 1:
        console.log("a=1");
        break;
    case 2:
        console.log("a=2");
        break;
    case 3:
        console.log("a=3");
        break;
}
```
#### 結果
```
a=2
```
#### 結論
當`輸入值`等於`選項`時  
執行該`選項`內的`動作`  
需要注意的是  
case 內的動作結束後要加上 break;  
不然下面的每個 case 都會被執行一次  
## 迴圈
### for
#### 基本語法
```javascript=
for (變數=初始值;變數<結束值;變數++){
    動作;
}
```
#### 範例
```javascript=
for (i=1;i<3;i++){
    console.log(i);
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
```javascript=
while (條件){
    動作;
}
```
#### 範例
```javascript=
int a=1;
while (a<3){
    console.log(a);
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
所以while (1){  
}  
就是無限迴圈  
### 特例
- break:
跳脫迴圈
- continue:
直接從下一圈開頭繼續
## 函式
### function
#### 基本語法
```javascript=
function 函式名稱(傳入值){
    return 回傳值;
}
```
#### 範例
```javascript=
function add(a,b){
    let c = a + b;
    return c;
}

console.log(add(1,2))
```
#### 結果
```
3
```
#### 結論
將重複使用的邏輯使用函式包裝起來  
方便用來重複呼叫  

### 函式應用 遞迴
#### 範例
```javascript=
let a = 1;
function fact(n){
    if (n === 0){
        return a;
    }else{
        a = n * a;
        n--;
        return fact(n);
    }
}

console.log(fact(5));
```
#### 結果
```
120
```
#### 結論
使用遞迴解決數學的階乘  
比起迴圈執行速度更有效率  

## 箭頭函式
javascript的特有用法  
#### 範例
```javascript=

```
#### 結果
```

```
#### 結論

