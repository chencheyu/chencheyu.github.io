---
date: 2025-02-20
publish: true
slug: aa3e467b-90ef-4165-9a58-0a398387ef38
tags:
- CS/Embedded
- CS/CAndCpp
title: Keil
---
## 簡介

## 编译函数或变量到指定地址

- 将函数加载到指定位置
  示例将 main.c 中的 delay 函数指定到 0x08020000 地址，可以在 c 文件中函数的定义处指定 delay 函数。
  `void delay(void) __attribute__ ((section(&quot;.ARM.__at_0x08020000&quot;)));`
- 将数组加载到指定位置
  `int Temp[] __attribute__ ((section(&quot;.ARM.__at_0x08020000&quot;))) = {0x1, 0x2};`
- 将变量加载到指定位置以 AT32F403AVGT7 为例：
  示例可以直接将 c 代码修改如下：
  `const int Temp __attribute__ ((section(&quot;.ARM.__at_0x08020000&quot;))) = 10; // RO`
  `int Temp __attribute__ ((section(&quot;.ARM.__at_0x20000000&quot;))) = 10; // RW`

## 加入 C Source File

![](CS/Embedded/Keil/29d34e27fd7ff69adc515e570f8579fb.png)User 右鍵 > Manage Project Item > Add Files
記得要選要加入的 Group，加入 C 檔即可，H 檔不用加

```
I2c
|-inc
    |-Source.h
|-src
    |-Source.c
```

建議維持此資料夾結構
