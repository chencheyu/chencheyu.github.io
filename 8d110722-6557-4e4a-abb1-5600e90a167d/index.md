---
date: 2019-05-18
publish: true
slug: a44e1e83-49dc-4835-87f6-d7df19fab154
tags:
- CS/Algorithm
title: Fisher Yates Shuffle
---
### 簡介

Ronald Fisher 和 Frank Yates 發明的均勻洗牌算法

### 算法

索引從0開始往len(卡排列表)遞增，索引i與隨機選擇的卡牌交換
隨機選擇的卡牌如果用rand() mod (len(卡排列表) - i)取隨機的卡牌，會不均勻
