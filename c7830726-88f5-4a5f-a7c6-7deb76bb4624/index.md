---
date: 2025-03-14
publish: true
slug: cbe6e463-2fae-404a-bb34-70457444fad8
tags:
- CS/Linux
- CS/Software
title: Desktop
uuid: 62dcad06-401a-4e38-85c6-c8253398f02a
---
## Software

Linux Only

### [Flameshot](https://flameshot.org/)

Linux 上的截圖工具，有任意矩形範圍，截圖後編輯（功能豐富），存檔檔名控制

#### Unable to capture screen

`xdg-desktop-por[3487]: Failed to show access dialog: GDBus.Error:org.freedesktop.DBus.Error.AccessDenied: GDBus.Error:org.freedesktop.DBus.Error.AccessDenied`
`Failed to associate portal window with parent window`
懷疑是 wayland 跟 Flameshot 配合不良導致
Flameshot doesn't work if launched from gui but works if launched from terminal

- Open Configuration

> - open the flameshot
> - click the flameshot icon on top right bar of ubuntu. do NOT click "Take Screenshot" yet, but click "Configuration" instead
> - with the flameshot configuration window opened, click the flameshot icon again on top right bar, this time click the "Take Screenshot"



實測有效

- [QtWayland](https://wiki.qt.io/QtWayland)
  `QT_QPA_PLATFORM=wayland`
  啟動 Flameshot 時傳遞 QT 環境變數
- [Wayland Help | Flameshot](https://flameshot.org/docs/guide/wayland-help/#can-t-screen-anything-on-wayland-gnome)
  install xdg-desktop-portal-gnome and xdg-desktop-portal
