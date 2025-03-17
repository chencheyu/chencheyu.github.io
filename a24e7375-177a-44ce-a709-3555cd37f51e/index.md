---
date: 2025-03-06
publish: true
slug: b72408b6-9e0b-44ba-b632-3ca54c4bebc9
tags:
- CS/Linux
title: USB
uuid: 6bc27603-d4a3-44cd-8446-10eaefd70605
---
## [Intel 為 eUSB2V2 準備 Linux 驅動](https://web.git.kernel.org/pub/scm/linux/kernel/git/gregkh/usb.git/commit/?h=usb-next&amp;id=c749f058b4371430a8338e1ca72b9ae38fef613b)

eUSB2V2 更新旨在為整合/嵌入式網路攝影機等裝置提供更多頻寬，以實現更高的分辨率，同時保持嵌入式 USB 的 1.2V 低功耗要求，在 Linux 6.15 引入

## [USB Everywhere | Hackaday](https://hackaday.com/2025/02/27/linux-fu-usb-everywhere/)

USB/IP 專案的目標是在 IP 網路上開發通用的 USB 設備共享系統。為了在計算機之間共享 USB 設備並保留其完整功能，USB/IP 將「USB I/O 訊息」封裝到 TCP/IP 負載中，並在計算機之間傳輸這些訊息
伺服器核心模組: usbip_core，usbip_host。您還需要usbipd（守護程式）
客戶端核心模組: vhci_hcd

### 伺服器

```sh
modprobe -a usbip_core usbip_host
usbip list -l   # -l for local
usbpip bind -b 4-3.1
```

Loading the modules
find a device to share
You’ll bind that device to the server

### 客戶端

```sh
modprobe -a vhci_hcd
usbip list -r myserver.local  # use your server name or IP
usbip attach -r myserver.local -b 4-3.1
```

Port number is somewhat dynamic across reboots
一旦設備連接，它看起來就像系統上的任何其他 USB 連接埠一樣

### [USBIP - ArchWiki](https://wiki.archlinux.org/title/USB/IP)
