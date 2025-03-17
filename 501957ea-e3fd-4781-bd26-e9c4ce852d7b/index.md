---
date: 2024-08-04
publish: true
slug: 2cefe8f4-226c-4fb1-b4a4-03c538dd9131
tags:
- CS/TheoryOfComputation
title: Optimizing Compiler
uuid: 589f6201-ef48-4f55-bca1-e1a544f61ac3
---
### 從零開始建構 C 語言最佳化編譯器

Jserv 在 Coscup 2024 的演講，基於 shecc
[從零開始建構 C 語言最佳化編譯器](https://hackmd.io/owo-6JRnRei2mGr64cfvZQ)

### basic block

程式碼單一入口，單一出口的區域

- 可達性 (reachability)
  除了起始節點外，若一個基本區塊在最佳化中沒有前任節點連接，則此基本區塊被稱為不可到達 (unreachable)，我們可安全的移除該基本區塊來簡化 CFG，如 C 語言關鍵字 break, continue, return 後的程式碼及 if, for, while 中條 件恆為 0 的情況。

- 支配性 (domination)
  若從起始點到節點 n 都必經節點 d，則稱節點 d 為節點 n 的支配節點 (dominator)，記作 d dom n;而其中最接近節點 n 的支配節點 m 又稱為直接支配 節點 (immediate dominator)，記作 m idom n。將 m 作為親代節點、n 作為子節點，我們可建立另外一種樹狀結構 ── 支配樹 (dominator tree)，記錄從起始點到某個基本區塊節點中必經的路徑。

結合可達性分析，若節點 n 不可到達，則其在支配樹中的所有子節點將同樣不可到達，這時我們可快速且安全地從 CFG 中移除這些基本區塊節點。

### [shecc](https://github.com/sysprog21/shecc)

shecc看起來很完善，有甚麼可以貢獻的東西 (2024)
[Issues | shecc](https://github.com/sysprog21/shecc/issues)

- 有好多 issue 可以解啊。
- c-preprocess 和 frontend 可以一起做R。
- bug 還是很多，也可以去找 bug 提出來。
- 產生的程式碼需要做 bootstrapping，目前只能跑在 QEMU，希望找些其他系統模擬的方法支援非 Linux OS
- 目前只支援 ARM／RISC-V，看看有沒有人可以貢獻 x86(-64) 之類的處理器後端。

#### 建構流程

Bootstrapping 分成三個階段，可自舉
stage0: 用 gcc/clang/MSVC 編譯，產生可執行檔 out/shecc，針對原生的處理器架構
stage1: 用 stage0 產生的程式編譯 shecc 原始程式碼，產生的執行檔 out/shecc-stage1.elf 是ArmV7 或 RISC-V 指令集
stage2: 用 stage1 產生的 out/shecc-stage1.elf 編譯自己
