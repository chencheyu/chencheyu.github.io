---
date: 2023-01-01
publish: true
slug: 8b5df7b1-756b-449b-8e6a-5ffd7f241de5
tags:
- CS/Security
title: CVE 2023
uuid: 28f851d2-98f6-4405-aee8-d4726b16d515
---
## Windows

### [CVE-2023-38831](https://nvd.nist.gov/vuln/detail/CVE-2023-38831)

> 6.23 之前的 RARLabs WinRAR 版本中已發現可利用的漏洞。該漏洞使攻擊者能夠透過特製的 ZIP 檔案執行任意程式碼。此漏洞是由於對包含良性文件（例如普通 .PDF 文件）以及共享相同名稱的資料夾的 ZIP 存檔處理不當而產生的。當使用者嘗試存取良性檔案時，存檔可能包括包含可執行內容的類似命名的資料夾。在嘗試存取良性文件期間會處理資料夾中的惡意內容，從而促進任意程式碼的執行。



更新 WinRAR 到高於 6.23 即可完全不受引響

- [CVE-2023-38831 PoC](https://github.com/HDCE-inc/CVE-2023-38831)

### CVE-2024-38074

9.8 分，遠端無授權執行
