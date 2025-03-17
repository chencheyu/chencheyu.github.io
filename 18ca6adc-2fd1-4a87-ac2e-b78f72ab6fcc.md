---
uuid: 858a9379-80e0-4019-8bf2-bf9eb6b562c8
tags:
  - CS/ComputerSystemOrganization/AMD
  - CS/Uefi
date: 2025-03-10
title: AMD Microcode
publish: false
---
## Microcode Update
AMD 產生了一個新的微碼補丁，補丁以二進位形式交付給 BIOS、OS 和其他合作夥伴；這個 blob 內部包含以下元件：
- 描述補丁頭格式、其設計的 CPU 的元資料、日期和版本資訊的標題。
- 2048 位元RSA PKCS `#1`簽章。
- 2048 位元 RSA 公鑰模數（0x10001 作為指數）。
- 公鑰的2048 位元 蒙哥馬利逆（用於簡化 RSA 模運算）。
- 指示補丁的其餘部分是否已加密的位元。
- 符合暫存器和遮罩值的數組，用於選擇要修補的微碼和指令。
- 一組捆綁在四個「四元組」中的微操作，每個微操作都與一個序列字配對，指示下一步執行的位置

一旦收到新的補丁，微碼將在運行時或下次重啟時加載。
- BIOS 或 OS 將識別正確的微碼補丁檔案（基於標頭中的 CPU 識別碼）並開始更新例程。
- 軟體將把微碼補丁 blob 的虛擬位址寫入 MSR 0xc0010020，這指示 CPU 微碼開始執行微碼更新程式。
- 微碼將補丁複製到內部記憶體，並驗證補丁的 CPU 識別碼是否與實際硬體的識別碼相符。
- 微碼檢查補丁的版本是否比目前安裝的補丁版本舊。如果是這樣，補丁就會被拒絕——這可以防止回滾攻擊。
- 該補丁使用 AES-CMAC 對 RSA 公鑰進行雜湊處理，並確認雜湊值與 AMD 在製造晶片時融合的值相符。
- 此補丁對補丁內容（匹配暫存器、指令遮罩和補丁指令）進行雜湊。
- 使用 RSA 公鑰和提供的 Montgomery 模數逆解密 RSA PKCS `#1` 簽章。結果是補丁內容的填充 AES CMAC 哈希。
- 如果簽署的雜湊值與計算的雜湊值匹配，則補丁內容將複製到內部 CPU 補丁 RAM 中。否則，補丁將被拒絕。
- CPU 微碼修補程式版本（MSR 0x8b）已更新以反映新安裝的修補程式。
AMD Zen CPU 使用幾乎標準的 RSASSA-PKCS1-v1_5演算法；但是，AMD並沒有使用建議的雜湊函數，而是選擇了容易發生衝突的 CMAC 函數

> \- [Zen and the Art of Microcode Hacking](https://bughunters.google.com/blog/5424842357473280/zen-and-the-art-of-microcode-hacking)

## [Reverse Engineering x86 Processor Microcode](CS/ComputerSystemOrganization/ReverseEngineeringX86ProcessorMicrocode.pdf)
