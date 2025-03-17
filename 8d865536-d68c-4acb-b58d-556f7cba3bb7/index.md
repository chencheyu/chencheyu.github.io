---
date: 2024-06-28
publish: true
slug: d6fb8a09-4c12-404b-81c9-448f84c9a015
tags:
- CS/Algorithm
title: Synchronization.md
---
## 簡介

檔案同步
目前有三種方法

- Lock
  將要修改的檔案鎖定，不允許其他程式修改，如果鎖沒有失效時間，可能導致崩潰程式永遠占用鎖
- Operational Transformation
  紀錄每個程式修改的每一行，並將記錄傳播給其他程式，基於 Operational Transformation
- [ Operational Transformation Frequently Asked Questions and Answers](https://web.archive.org/web/20200623064915/https://www3.ntu.edu.sg/home/czsun/projects/otfaq/)
- [Concurrency Control in Groupware Systems](../34dd250a-fba2-4a93-9fd9-9f9d10b89bc6.pdf)
  原始論文
- Three-way Merge

> 1. 客戶端將文件的內容傳送到伺服器。
> 2. 伺服器執行三向合併以提取使用者的變更並將其與其他使用者的變更合併。
> 3. 伺服器將文件的新副本傳送給客戶端



半雙工系統，Subversion 使用此方法

- Differential Synchronization

## Differential Synchronization

[Differential Synchronization](https://neil.fraser.name/writing/sync/)
差異同步是一種對稱演算法，它透過不斷循環的背景比對（diff）與修補（patch）操作來保持兩個文件的同步

### 資料流概覽

理想化的差異同步資料流如下所示，假設兩個文件（分別稱為「客戶端文本」與「伺服器端文本」）位於同一台電腦上，沒有網路延遲的影響

1. 比較 Client Text 與 Common Shadow，計算 Diff
   這會回傳 Client Text 相較於 Common Shadow 的變更（編輯操作列表）
2. 將 Client Text 的內容複製到 Common Shadow
   必須確保此複製的內容與**第一步**時的 Client Text 完全相同，在多執行緒環境中，應先對文本進行快照（snapshot）
3. 應用 Diff 變更至 Server Text（最佳努力方式）
   嘗試將編輯操作套用到 Server Text，允許部分變更可能因為內容變動而失敗
4. 更新 Server Text
   伺服器端文本應用變更，這個步驟必須**原子性**（atomic），但不一定要阻塞（blocking），可多次嘗試，直到 Server Text 穩定。
5. 對 Server Text 進行對稱的反向同步
   現在，Common Shadow 代表的是前一次同步時的 Client Text，透過相同的流程，比對 Server Text 與 Common Shadow，獲取 Server Text 的變更，並將這些變更應用回 Client Text。
   Shadow 是指之前存下的狀態

### Dual Shadow

前面介紹的差異同步（Differential Synchronization）方法是最基本的形式，但它無法直接應用於客戶端-伺服器（Client-Server）架構，因為同步過程中使用的共同影子（Common Shadow）會成為共享狀態，這在分佈式系統中難以保持一致性

- 每個節點都維護一份獨立的影子副本：
  - 客戶端文本（Client Text） 需要對應一個伺服器影子（Server Shadow）
  - 伺服器文本（Server Text 需要對應一個客戶端影子（Client Shadow）
- 同步流程仍然是雙向進行的：
  - 第一階段：將 Client Text 的變更應用到 Server Text，並同步 Client Shadow
  - 第二階段：將 Server Text 的變更應用到 Client Text，並同步 Server Shadow
- 影子副本與對應的文本必須在每個同步週期後完全一致：
  - (v1 Diff v2) Patch v1 == v2（即，應用變更後，影子副本應該與最新的文本完全匹配)
  - 影子副本的變更應該是精確匹配的（fragile patches），而文本的變更應該是模糊匹配的（fuzzy patches)
