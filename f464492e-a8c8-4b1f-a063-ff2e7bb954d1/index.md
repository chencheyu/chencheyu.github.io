---
date: 2024-04-12
publish: true
slug: 5a86cbd9-b1cf-4481-8f6f-0647305e0497
tags:
- CS/Security
title: CVE 2024
---
## 簡介

紀錄知道的漏洞

## Linux

### [CVE-2024-1086](https://nvd.nist.gov/vuln/detail/CVE-2024-1086)

Linux netfilter nf_tables元件中存在釋放後使用漏洞，可被利用來實現本機權限提升。nf_hook_slow() 被二次釋放

### [CVE-2024-3094](https://nvd.nist.gov/vuln/detail/CVE-2024-3094)

Open sshd 使用的 XZ Utils 被匿名貢獻者加入惡意程式碼，在正式 release 前被發現，只要確定沒使用到測試版的 Open sshd 即不會被引響

- [WIP How to extract the malware payload](https://hackmd.io/@cve-2024-3094/how-to-extract-the-malware-payload)
- [Everything I know about the XZ backdoor](https://boehs.org/node/everything-i-know-about-the-xz-backdoor)
  教學文章，如何安全的利用套件安裝程式取出有風險的樣本

### [CVE-2023-6546](https://nvd.nist.gov/vuln/detail/CVE-2023-6546)

Linux kernel n_gsm(只有 tty 會使用到) 存在提權漏洞
[New Linux LPE via GSMIOC_SETCONF_DLCI](https://www.openwall.com/lists/oss-security/2024/04/10/18)

1. YuriiCrimson's version (April 6-ish)
   It seems to use GSMIOC_SETCONF_DLCI, PoC supposedly works on current Ubuntu and Debians, but is stopped by LKRG.
   PoC and writeup are here: [ExploitGSM](https://github.com/YuriiCrimson/ExploitGSM/tree/main)
2. jmpeaux' version (March 21)
   This seems similar, also using GSMIOC_SETCONF_DLCI. In the screen shots, even the working dir for the PoC is identical to 1). Yurii claims jmpeaux stole his work.
   Writeup: [The-tale-of-a-GSM-Kernel-LPE](https://jmpeax.dev/The-tale-of-a-GSM-Kernel-LPE.html)
   PoC: [GSM_Linux_Kernel_LPE_Nday_Exploit](https://github.com/jmpe4x/GSM_Linux_Kernel_LPE_Nday_Exploit/tree/main)
3. ZDI-24-020 / CVE-2023-6546 (January)
   This also exploits a race condition resulting UAF in the gsm_dlci struct. It's a little older.
   Writeup and PoC: [Nassim-Asrir-ZDI-24-020](https://github.com/Nassim-Asrir/ZDI-24-020/)

## Windows

### [CVE-2024-4577 - PHP CGI Argument Injection Vulnerability](https://labs.watchtowr.com/no-way-php-strikes-again-cve-2024-4577/)

任意命令執行，在 Windows 下利用 CGI 執行 hph 的網頁服務

- PHP 8.3 < 8.3.8
- PHP 8.2 < 8.2.20
- PHP 8.1 < 8.1.29
  And
  Windows 語系為
- Traditional Chinese (Code Page 950)
- Simplified Chinese (Code Page 936)
- Japanese (Code Page 932)
  皆受引響(XAMPP 安裝預設)
  攻擊利用傳遞字符 0xAD ([Soft Hyphen](CS/Backend/Unicode)) 替代 0x2D (normal dash) 跳過 php cgi 的跳脫

> 閱讀 Orange 的博客，很明顯該錯誤僅影響 PHP 的 CGI 模式。在此模式下，Web 伺服器解析 HTTP 請求並將其傳遞給 PHP 腳本，然後 PHP 腳本對其執行一些處理。例如，查詢字串在命令列上被解析並傳遞給 PHP 解釋器 -例如，請求 `http://host/cgi.php?foo=bar` 可能會被執行為。`php.exe cgi.php foo=bar`
> 這裡的一個重要細節是 Apache 將轉義實際的連字符 0x2D 但不會轉義第二個 highlighted (0xAD)。畢竟，它不是真正的連字符，對吧？所以沒必要轉義……對吧？
> 如果我們為 CGI 處理程序提供軟連字符 (0xAD)，CGI 處理程序將不會覺得需要轉義它，並將其傳遞給 PHP。然而，PHP 會將其解釋為真正的連字符，這使得攻擊者可以將以連字符開頭的額外命令行參數偷偷帶入 PHP 進程
> 注入以下參數 `-d allow_url_include=1 -d auto_prepend_file=php://input`
> 這將接受 HTTP 請求正文的輸入，並使用 PHP 對其進行處理。足夠簡單讓我們嘗試一個配備 0xAD 而不是通常的連字符的版本



```jsx
POST /test.php?%ADd+allow_url_include%3d1+%ADd+auto_prepend_file%3dphp://input HTTP/1.1
Host: {{host}}
User-Agent: curl/8.3.0
Accept: */*
Content-Length: 23
Content-Type: application/x-www-form-urlencoded
Connection: keep-alive

<?php
phpinfo();
?>
 
```

我們獲得了一個phpinfo頁面

### [CVE-2024-30078](https://nvd.nist.gov/vuln/detail/cve-2024-30078)

Windows Wi-Fi 驅動程式遠端程式碼執行弱點
未經驗證的攻擊者可以將惡意的網路封包傳送至使用 Wi-Fi 網路介面卡的相鄰系統，進而能從遠端執行程式碼

> 總之，此 CVE 的影響似乎遠沒有 Microsoft 通報中最初建議的那麼嚴重。利用它需要與目標位於同一網路上，暴力破解特定的記憶體佈局
> [basic concept for the latest windows wifi driver CVE](https://github.com/blkph0x/CVE_2024_30078_POC_WIFI)



### [NVD - CVE-2024-8811](https://nvd.nist.gov/vuln/detail/CVE-2024-8811)

WinZip 網路標記繞過漏洞
When opening an archive that bears the [Mark-of-the-Web](https://en.wikipedia.org/wiki/Mark_of_the_Web), WinZip removes the Mark-of-the-Web from the archive file. Following extraction, the extracted files also lack the Mark-of-the-Web

## Web

### [cdn.polyfill.io](https://polykill.io/)

polyfill.io 是瀏覽器相容的開源js 函式庫，`cdn.polyfill.io` 是最主要的 CDN，該 CDN 遭到供應鏈攻擊，會意外轉址到惡意網站

### [Confusion Attacks: Exploiting Hidden Semantic Ambiguity in Apache HTTP Server](https://blog.orange.tw/posts/2024-08-confusion-attacks-ch/)

Apache HTTP Server 的大量漏洞

1. **CVE-2024-38472** - Apache HTTP Server on Windows UNC SSRF
2. **CVE-2024-39573** - Apache HTTP Server proxy encoding problem
3. **CVE-2024-38477** - Apache HTTP Server: Crash resulting in Denial of Service in mod_proxy via a malicious request
4. **CVE-2024-38476** - Apache HTTP Server may use exploitable/malicious backend application output to run local handlers via internal redirect
5. **CVE-2024-38475** - Apache HTTP Server weakness in mod_rewrite when first segment of substitution matches filesystem path
6. **CVE-2024-38474** - Apache HTTP Server weakness with encoded question marks in backreferences
7. **CVE-2024-38473** - Apache HTTP Server proxy encoding problem
8. **CVE-2023-38709** - Apache HTTP Server: HTTP response splitting
9. **CVE-2024-36387** - Apache HTTP Server: DoS by Null pointer in websocket over HTTP/2

> 整個 Httpd 的服務需要由數百個小模組齊心合力，共同合作才能完成客戶端的 HTTP 請求，官方所列出的 136 個模組其中約有快一半是預設啟用或經常被使用的模組！
> 而更令人驚訝的是，這麼多模組在處理客戶端 HTTP 請求的時候，彼此之間還要共同維護著一份非常巨大的 request_rec 結構。 這個結構包括了在處理 HTTP 時會用到的一切元素，詳細的定義可以從 include/httpd.h 中找到。 所有模組都依賴這個巨大的結構去同步、溝通，甚至交換資料。 這個內部結構會像是拋接球般在所有模組間傳遞來傳遞去，每個模組都可以根據自己的喜好去隨意修改這個結構上的任意值！
> 所以我們的出發點很簡單 —— **模組間其實並不完全了解彼此的實作細節，但卻又被要求要一起合作**。 每個模組可能由不同的開發者實作，程式碼歷經多年的疊代、重整以及修改，它們真的還清楚自己在做什麼嗎？ 就算對自己瞭若指掌，那對其它模組呢？ 在缺乏一個好的開發標準或使用準則下，這中間必然會存在很多小縫隙是我們可以利用的！



## Hardware

### [CVE-2024-56161](https://bughunters.google.com/blog/5424842357473280/zen-and-the-art-of-microcode-hacking)

允許執行任意 [Amd Microcode](../6eab4e38-d4bb-4ce5-948e-52f791bd7722.md) 更新程式。此缺陷源自於 AMD 在Microcode簽章驗證期間使用 CMAC 函數作為Hash，而該函數容易發生衝突。透過利用此弱點，攻擊者可以偽造 RSA 公鑰和簽章，從而繞過安全措施
EntrySign漏洞的安全性影響有限，因為攻擊者必須先獲得主機 Ring 0 存取權才能安裝 Microcode 更新，並且這些更新不會在電源循環後持續存在
