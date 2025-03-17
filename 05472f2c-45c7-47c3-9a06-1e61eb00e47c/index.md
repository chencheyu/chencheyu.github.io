---
date: 2025-03-05
publish: true
slug: 39d812bc-a700-4370-ab1b-0097c9dc8efa
tags:
- CS/Security
title: CVE 2025
uuid: 693a84f1-cf67-4ad8-81d6-98cde3619171
---
## [ToDesktop 的 Firebase 服務管理員帳戶權限洩漏導致可以任意更新 ToDesktop 部屬的程式](https://kibty.town/blog/todesktop/)

建立容器具有比必要更廣泛的權限，允許 `postinstall` 應用程式中的腳本 `package.json` 檢索 Firebase 憑證，從而導致憑證洩漏，這將允許攻擊者存取 ToDesktop 資料庫、使用者帳戶並對任意應用程式部署未經授權的更新
