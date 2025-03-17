---
date: 2018-04-10
publish: true
slug: 4ad37e09-1480-4313-beb2-2cc6fe6c717c
tags:
- CS/TheoryOfComputation
title: "\u7A0B\u5F0F\u8A9E\u8A00"
uuid: 7d32ff96-a5a4-45ae-ae32-d85667218c99
---
### 簡介

大學時程式語言課程的上課筆記

### 記憶體管理議題

#### ada

動態的他會收回去

#### c/c++

自己管，指標可以指向任何地方(通常拿來做記憶體管理)
指標可移動
須明確取參
參照像const pointer

#### c#

僅參照

### 堆積管理

可動或固定大小

#### 收回方式

1.紀錄多少人參照到，沒就收回
有參照循環議題
2.直到沒記憶體才回收，回收時檢查是否有參照到

### 型態確定

assign or function or operator 檢查
需有相容的概念(可隱含轉換)
強型別:編譯期檢查全部型別 如ada(可以關)、jave、c#

## 運算式

運算子結合率(變數 > 常數 > 小括號)

如果函式會改變變數值，先後很重要
解1:不准改
解2:給定方向(如java)

結合方向

#### ruby

凡是多是方法

### Overloading operator (重載運算子)

C++
潛在問題

```c++
    int *a,a;
    c=b*a;
```

指標||乘法 (???)
無法檢查!!!
矩陣乘法，還是元素相乘

### 轉型

不能轉
ada
明確型態轉換
C: (int) angle
python: int(angle) base 10 十進位轉換

### overflow(太大超過) || underflow(太小無法表示)

exception : catch 解決

### 關聯運算式

強制轉換
c:明寫，算到知道答案就不算了
(a<b<c) != (a<b && b<c)
rudy: 用== 跟=?分辨轉型

### 指派(assignment)

ada用(:=)
if(a=b) //ERROR 語意錯誤(bug)
c中 a+=d 同於 a=a+b
