---
date: 2018-11-14
publish: true
slug: 119c3c4a-c975-4e32-b258-a005219c70cc
tags:
- CS/Embedded
title: Microprocessor Mid-term Project.md
---
## target

我相信你們大家多看過
chrome://dino/
![](../200651dc-a3b0-4d6b-8b0d-46bc90f18849.jpg)
就復刻一個，應該會在uart上，但RJ-433的2.5mb/s讓人恐懼
如果寫不上去就去LCD(應該是兩個點)，計分會用七段顯示器。
蹲下可以，腳不會動。

## 元件

timer,鋒鳴器，uart,按鈕，七段顯示器

## 程式結構!

![](../1ff231fc-d19f-4067-99e8-3f73a2cec09e.jpg)

## 流程

```flow
st=>start :刻元件介面
e=>end: debug
op=>operation:  lowlevel print function(緩衝區，分頁選擇器，協議)
op2=>operation: 顯示api
op1=>operation: main
c0=condition:耦合測試
st->op->op2->po1->c0
c0(fail)->st
c0(pass)->e
```

這是時間跟達成率的關西 **[e^x + cos(x)](https://www.wolframalpha.com/input/?i=e%5Ex%2Bcosx)**

我原本想做弊，結果他不是javastript QQ

![](../3af8e615-0a9d-424f-b301-5573f323edda.png)

search "Atari Breakout" in google  picture
![](../ae8dcae7-abbd-4153-9b29-ad43f3d699ae.png)
如果我有空想重操舊業算算彈性碰撞的話，完全沒有實踐的想法。

> Java 是個很棒的語言
> 對 C++ 社群有非常大的貢獻
> 他收留了所有寫不好 C++ 的人
> 維持了 C++ 神聖中土上高貴住民的純粹血統



所以我去寫java
