---
tags: 筆記, 演算法
---

# 動態規劃 dynamic programming

## 範例：費氏數列

費氏數列是一個需要重複多次運算的數列  
但我們可以儲存已經算好的值來節省重複計算的時間  

- 動態規劃範例：使用陣列存放資料
```cpp=
#include <iostream>
using namespace std;
int array[20];

void f(int input){
    if(input == (0 | 1)){
        array[input] = 1;
    }else{
        array[input] = array[input-2] + array[input-1];
    }
}

int main() {
  for(int i=0;i<20;i++){
    f(i);
  }  
  for(int i=0;i<20;i++){
    cout << array[i] << endl;
  }
  return 0;
}
```

上面的程式中因為把計算的結果都存在array中  
大幅縮小了需要重複計算的時間  

時間複雜度從 O(2<sup>n</sup>) 降低到了 O(n)  
只需要把空間複雜度增加 O(n) 用於儲存計算過的資料  

- 使用兩個變數存放資料
下面這個寫法同樣可以達到不需重複記算的效果  

```cpp=
#include <iostream>
using namespace std;

int main() {
  int count = 1;
  int ans = 1;
  cout << count << endl << ans << endl;
  for(int i=0;i<10;i++){
      count = count + ans;
      cout << count << endl;
      ans = count + ans;
      cout << ans << endl;
  }
  return 0;
} 
```

使用兩個變數來儲存下一個數字需要的兩筆資料  
當第N筆資料被計算出來後就把第N-2筆資料取代  
這樣就可以只使用兩個變數的空間  
但是在程式的其他地方就不能直接去呼叫隨機一筆資料  
因為計算結束後只會保存最後兩筆資料  

- 最不理想的計算方法 每筆資料都重新求一次
如果不用陣列來儲存計算過的資料會需要花大量時間來計算重複的項目  
就像下面的範例一樣  

```cpp=
#include <iostream>
using namespace std;

int f(int input){
    if(input == 1 || input == 0){
        return 1;
    }
    return f(input-1) + f(input-2);
}

int main(){
    cout << f(20);
    return 0;
}
```