---
date: 2024-12-20
publish: true
slug: cf8e5f13-a6de-4624-9e14-975a34df1b86
tags:
- CS/Algorithm
title: Blum Blum Shub
---
### 簡介

[Blum, Blum & Shub](http://www.ciphersbyritter.com/NEWS2/TESTSBBS.HTM)
一種偽隨機數產生器
$\displaystyle x_{n+1}=x_{n}^{2}{\bmod {M}}$, $M = pq$ ,  p and q are not factors of $x_{0}$
第 i 項的疊代公式

$\displaystyle x_{i}=\left(x_{0}^{2^{i}{\bmod {\lambda }}(M)}\right){\bmod {M}}$

```python
p = 11
q = 23
x = 3
for i in range(10000):
    x = (x ** 2) % (p * q)
```

```js
[9, 81, 236, 36, 31, 202, 71, 234, 108, 26, 170, 58, 75, 59, 192, 179, 163, 4, 16, 3]
```
