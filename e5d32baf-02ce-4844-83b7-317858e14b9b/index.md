---
publish: true
slug: 2ce7e117-3534-480a-9098-df0f92c6d669
tags:
- CS/Windows
title: SymbolicLink
uuid: 938dc5f1-78b0-4c8d-93f3-d65e18aeb553
---
Windows 無法在未使用uac提權的前提下建立軟連結(即使有資料夾完全控制權限也不行)，但可以以以下方式繞過:

- 開啟開發者模式
- mklink 應該也可以繞過(待確認)
