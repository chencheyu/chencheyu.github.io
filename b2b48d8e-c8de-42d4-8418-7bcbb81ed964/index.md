---
date: 2024-06-21
publish: true
slug: 3e809070-d9f0-4c16-bb4d-e8a777ddec32
tags:
- CS/Windows
title: Windows.md
---
[PE](../aced79f2-f880-4aba-a6c9-96ec8656b635.md)
[Path](../fb4a3895-4d9e-4bf9-9aa3-793c4edba7eb.md)
[_MinGW32](CS/Windows/_MinGW32.md)
[CSharp](../c2bd8c22-9200-4e77-9436-1215d9620693.md)
[WindowsApiSet](../a7e8ae6e-3e00-42a0-924a-df2cf070acd4.md)
[BypassWindowsDefender](../772cf18e-62ae-4e48-a846-044fbeffa2a9.md)

## [暫停微軟更新100年（win10 / 11適用）](https://forum.gamer.com.tw/C.php?bsn=60030&amp;snA=650231)

```sh
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsUpdate\UX\Settings]
"PauseFeatureUpdatesStartTime"="2024-01-01T00:00:01Z"
"PauseQualityUpdatesStartTime"="2024-01-01T00:00:01Z"
#暫停功能更新與重大更新的起始時間(GMT時間)
"PauseFeatureUpdatesEndTime"="2124-01-01T00:00:01Z"
"PauseQualityUpdatesEndTime"="2124-01-01T00:00:01Z"
#暫停功能更新與重大更新的到期時間(GMT時間)
"PauseUpdatesStartTime"="2024-01-01T00:00:01Z"
"PauseUpdatesExpiryTime"="2124-01-01T00:00:01Z"
#暫停自動更新的起始與到期時間(GMT時間)
```

## [Tftpd64](https://pjo2.github.io/tftpd64/)

IPv4 and IPv6 server for DHCP, TFTP, DNS, SNTP and Syslog on windows
需要先啟動服務 `.\tftpd64_svc.exe -debug`  or

```sh
.\tftpd64_svc.exe -install
net start Tftpd32_svc
```

然後才可以用打開 GUI `tftpd64_gui.exe`

可以設定成 [PXE](https://github.com/tianocore/tianocore.github.io/wiki/PXE) Server

## [New Technologies File System (NTFS)](<https://github.com/libyal/libfsntfs/blob/main/documentation/New%20Technologies%20File%20System%20(NTFS>).asciidoc)

[NewTechnologiesFileSystem](../90a63c13-a134-4e26-a9f5-fc47bbfaa8af.asciidoc)
libfsntfs 的 NTFS 格式逆向紀錄文件

### MFT

NTFS 使用主文件表 (MFT) 來儲存有關檔案和目錄的資訊。 MFT 條目引用不同的磁碟區和檔案系統元資料
通常包含已刪除的檔案資訊

## Windows 上開發求生

### Node.js On Windows

請用 [nvm](https://github.com/coreybutler/nvm-windows) 作為 node.js 版本管理工具，直接安裝會弄亂原本的 Python 環境(對他會幫你裝Python)，nvm 只能用 cmd 執行

### [Microsoft Learn](https://learn.microsoft.com/en-us/)

前稱 MSDN 微軟官方文件的集散地

### Require UAC

讓程式在執行時主動請求使用者給 UAC
屬性>連結器>資訊清單檔>UAC執行層級
設為 requireAdminstrator

### Visaul Studio 20xx 加入外部 DLL

需要準備 abc.h,abc.dll,abc.lib

- 在方案管理中加入現有項目將準備的檔案加入
- 注意 abc.dll,abc.lib 的屬性 abc.lib 必須式函式庫  abc.dll 不參與建置
- 屬性>連結器>輸入>其他相依性中追加 abc.lib
- 屬性>建置事件>建置後事件>命令列 加上 `xcopy /y /d &quot;abc.dll&quot; &quot;$(OutDir)&quot;` (每一個建置目標都要設一次)
  [Create and use your own Dynamic Link Library](https://learn.microsoft.com/en-us/cpp/build/walkthrough-creating-and-using-a-dynamic-link-library-cpp)

### Visaul Studio 20xx 找不到或無法開啟 PDB

- 選項>調試>常規>啟用源服務器支持
- 選項>調試>符號> Windows 符號服務器
  開啟以上兩個選項

### 找不到 VCruntime140D.dll

VCruntime140.dll 在 Microsoft Visual C++ 20xx Redistributable 中，直接下載安裝
VCruntime140D.dll 在 Visaul Studio 20xx 安裝時附帶，你一定 build 到 debug 版，據說把執行階段程式庫設成 `/MD` 有用，但我試沒有用

### Syntax Error Identifier On BOOL, UCHAR, USHORT, ULONG, PBYTE

`#include &lt;windows.h&gt;` 在主程式

### 程式亂碼

嘗試用 chcp 切換頁碼如 `chcp 950`(big5)
需要開 CMD 下 chcp 後再執行程式
不保證有效

### [InsideClipboard](https://www.nirsoft.net/utils/inside_clipboard.html)

Windows 剪貼簿記debug 工具

## 無線網路報告

```sh
netsh wlan show wlanreport
```

告包含下列區段

- Network adapters
- `IPConfig /all`
- `NetSh WLAN Show All`
- `Profile Output`
- `Session Success/Failures`
- Wireless Sessions

### [Intel Wi-Fi 6E 或 Wi-Fi 7 產品啟用 6 GHz 頻帶](https://www.intel.com/content/www/us/en/support/articles/000059385/wireless/intel-wi-fi-6e-products.html)

另請注意，某些國家的監管機構禁止使用 6 GHz 頻帶。系統製造商也可能未在您的平台上啟用此功能。Intel 建議您檢查您所在國家/地區的法規是否允許使用 6 GHz 頻段，以及系統製造商是否已在您所在國家/地區啟用支援 6 GHz 頻段的設備。

開啟 6 GHz 頻帶的要求：
確保您的系統是在 Windows 11 上運行Microsoft包括 Microsoft 提供的最新更新。
使用 Intel® 無線網路介面器的最新 Wi-Fi 驅動程式：

- Intel® Wi-Fi 6E （Gig+） 產品： 版本 22.70.0 或更高版本
- Intel® Wi-Fi 7 產品： 版本 23.10.0 或更高版本

要求：

- 需要與Wi-Fi 6E或Wi-Fi 7相容的路由器才能訪問6 GHz頻帶。
- 需要與Wi-Fi 7相容的路由器和 Windows 11 24H2（或更高版本）操作系統才能啟用Wi-Fi 7 功能。

## 跳過 Windows 11 OOBE 強制連網

- Shift + F10 or Shift +F10 + Fn 叫出 Cmd
- Cmd 輸入 `oobe\bypassnro`

## Windows 產品金鑰

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SoftwareProtectionPlatform\BackupProductKeyDefault`
查看主機板金鑰的方法只適用於許可是OEM的設備及品牌機預裝的windows系統，如果您的 Windows 是通過數位許可證啟動的（例如通過 Windows 10 免費升級），則不會有原始產品金鑰

## win 筆電無休眠 / 睡眠

- 先拔掉充電器，再合蓋
- 將電腦調整為休眠模式 (不會被鍵盤或滑鼠喚醒)
  `powercfg /hibernate on`
- 裝置管理員找到你懷疑會喚醒電源的外設，找到允許此裝置喚醒計算機，並取消勾選該選項
- 電源選項 > 電源與睡眠設定 > 進階電源設定 > 停用允許喚醒計時器

## Clear Icon Cache and Thumbnail

如果應用程式圖標變為白紙圖標有可能是 Icon Cache 損壞，需要清除後重啟
Icon Cache 在 `%userprofile%/AppData/Local/IconCache.db`，直接刪除
Thumbnail 開啟磁碟清理工具選系統碟找到 Thumbnail 選項勾選後清除
