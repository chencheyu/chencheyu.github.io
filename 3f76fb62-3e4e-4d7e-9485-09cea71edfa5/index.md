---
date: 2024-05-10
publish: true
slug: 57d2c52d-a9ac-49d4-a80a-2384ca2e7785
tags:
- CS
title: Brainfuck.md
uuid: 80ac015e-73f4-414a-81b0-8b9023e213ee
---
### 簡介

一個由 8 支指令組成的圖靈完備程式語言

- `&gt;` 	Increment the pointer.
- `&lt;` 	Decrement the pointer.
- `+` 	Increment the byte at the pointer.
- `-` 	Decrement the byte at the pointer.
- `.` 	Output the byte at the pointer.
- `,` 	Input a byte and store it in the byte at the pointer.
- `[` 	Jump forward past the matching `]` if the byte at the pointer is zero.
- `]` 	Jump backward to the matching `[` unless the byte at the pointer is zero.
  有一個有限長度的連續記憶體，及一個指針來表明當前指令要操作的區塊

[BrainFuck Programming Tutorial by: Katie](https://gist.github.com/roachhd/dce54bec8ba55fb17d3a)

### awesome

- [Brainfuck-An Eight-Instruction Turing-Complete Programming Language](https://www.muppetlabs.com/~breadbox/bf/)
- [Index of brainfuck](http://esoteric.sange.fi/brainfuck/)
  Brainfuck 實作及程式收集
- [some brainfuck fluff by daniel b cristofani](https://brainfuck.org/)
- [Brainfuck](https://esolangs.org/wiki/Brainfuck)
  Esolangs Wiki
- [`Brainf***`](https://www.iwriteiam.nl/Ha_BF.html)
- [`brain------------------------------------------------------fuck.com`](https://web.archive.org/web/20170913173425/http://www.brain------------------------------------------------------fuck.com/)

### Portable

[Portable Brainfuck](https://www.muppetlabs.com/~breadbox/bf/standards.html)

> - 元胞數組的實際大小是實現定義的。但是，該數組應始終包含至少 9999 個單元。 （允許大小小至 4 位數字是為了程式設計師用三行 C 程式碼等編寫解釋器的好處。）
> - 如果程式嘗試將指標移到第一個陣列單元下方或最後一個陣列單元之外，則該程式的行為是未定義的。 （一些實現會導致指標迴繞，但許多（也許是大多數）實現的行為方式與 C 指標漫遊到任意記憶體一致。）
> - 單一單元格可以包含的值的範圍是實現定義的。 （範圍也不必一致：考慮「bignum」實現的情況，其單元格的範圍僅受當前可用資源的限制。）但是，每個單元格的範圍應始終至少包括值 0 到127，含在內。
> - 如果程式嘗試將單元格的值減少到其記錄的最小值（如果有）以下，或將單元格的值增加到其記錄的最大值（如果有）以上，則執行此類操作後單元格中的值將執行 -定義的。 （大多數實作選擇讓值以 C 整數典型的方式環繞，但這不是必需的。）
> - 如果程式在輸入流程中沒有更多資料時嘗試輸入值，則此類操作後目前儲存格中的值是實現定義的。 （最常見的選擇是儲存 0 或儲存 -1，或保持儲存格的值不變。對於希望實現可移植性的程式設計師來說，這通常是最成問題的問題。）
> - 如果程式包含一個或多個不平衡括號，則程式的行為是未定義的。 （事實上，許多 Brainfuck 編譯器會在編譯過程中崩潰。）（不，我不會在這裡正式描述「不平衡」的含義。你們都知道它意味著什麼。）



[some little programs for testing brainfuck implementations](https://brainfuck.org/tests.b)
[測試 Brainfuck 記憶體位寬](https://github.com/rdebath/Brainfuck/blob/master/bitwidth.b)

### Compiler

- [bf-compiler](https://github.com/folkertvanheusden/bf-compiler)
  Brainfuck 編譯成其他語言
- [Esotope Brainfuck Compiler](https://github.com/lifthrasiir/esotope-bfc/tree/master)
  將 Brainfuck 編譯成可讀的 C
- [Brainfuck interpreters and compiler with Brainfuck torture test](https://github.com/rdebath/Brainfuck/tree/master)

> Brainfuck interpreters and compilers to C, V. VIM syntax file for brainfuck. Fast JIT Assembly, JIT C running, Perl, Python, php, Ruby, lua, go, awk, neko, PS1, bash, ook, trollscript etc



有很多供測試用的 Brainfuck 小程式

- [Design and Implementation of a 256-Core BrainFuck Computer](../7e43d64d-fd3c-42b7-b9b0-d6585efd0d00.pdf)

### [control flow in brainfuck](http://calmerthanyouare.org/2016/01/14/control-flow-in-brainfuck.html)

> 它唯一的控制流語句也兼作執行算術比較的唯一方法
> `[]` 大致相當於：



```c
while (x != 0) {
}
```

### `IF x != 0`（破壞性）

```c
x = read()
if (x != 0) {
    write(x)
}
```

等價於

```c
x = read()
while (x != 0) {
    write(x)
    while (x != 0) {
        x = x - 1
    }
}
```

`,[.[-]]`

### Optimize

- [bf](https://github.com/mrjameshamilton/bf)

- [bfoptimization](https://github.com/matslina/bfoptimization)

- [awib](https://github.com/matslina/awib)

> a brainfuck compiler written in brainfuck



> Research on how to best optimize brainfuck code.
> 生成 brainfuck to c ，用 python 寫成



> An optimizing brainfuck compiler with multiple target backends: JVM, smali, dex, C, LLVM IR, ARM, WASM, JavaScript and Lox.
> [brainfuck optimization strategies](http://calmerthanyouare.org/2015/01/07/optimizing-brainfuck.html)



跟 bfoptimization 同一個作者

> - `-、&gt;、&lt; 、+` 序列被收縮為單一指令。例如，`----`被替換為單一 SUB(4)
> - 相互取消的指令減少。例如，`+++--&gt;&gt;&lt;`相當於`+&gt;`並進行相應編譯。
> - 一些常見的結構被識別並用單一指令替換。例如`[-]`被編譯成單一SET(0)。
> - 已知永遠不會進入的循環將被刪除。這是在程式一開始打開的循環（當所有單元格都是 0 時）和在另一個循環關閉後立即打開的循環的情況。
> - 複製和乘法循環被替換為恆定時間運算。例如`[-&gt;&gt;+++&lt;+&lt;]`被編譯成兩個 RMUL(2, 3), RMUL(1,1)), SET(0)



### Algorithms

- [Large number](https://www.iwriteiam.nl/Ha_bf_numb.html)
  產生大數字的寫法
- [Brainfuck algorithms](https://esolangs.org/wiki/Brainfuck_algorithms)
- [An introduction to programming in BF](https://www.iwriteiam.nl/Ha_bf_intro.html)

### Turing Complete

- [Daniel B Cristofani 在 Brainfuck 中實現通用圖靈機提供了模擬證明](https://brainfuck.org/utm.b)
- [BF is Turing-complete](https://www.iwriteiam.nl/Ha_bf_Turing.html)
