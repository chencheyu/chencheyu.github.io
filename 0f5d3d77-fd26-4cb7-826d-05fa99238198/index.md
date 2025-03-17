---
date: 2023-05-05
publish: true
slug: c2635887-900c-4063-ac99-718bef3dfb5d
tags:
- CS/NetWork
title: DNS.md
uuid: e2e16658-59ad-401c-8ebf-538361447939
---
### acme.sh

[ACME Shell script](https://github.com/acmesh-official/acme.sh)
[acme-sh doc](https://github.com/acmesh-official/acme.sh/wiki/dnsapi#18-use-gandi-livedns-api)
確定能用的純Bash Script要SSL憑證命令行工具，確定Let's Encrypt可用，可以自動RENEW及搬憑證指定路徑

### Server

- [Technitium](https://technitium.com/)
  用 C# 寫的 DNS Authoritative, Recursive server，可以在 Windows 及 Linux 上執行
- [MaraDNS](https://github.com/samboy/MaraDNS)
  單一可執行檔，全部文字設定檔的 DNS Authoritative, Recursive server
- [CoreDNS](https://github.com/coredns/coredns)
  用 Goland 寫的 DNS Authoritative, CoreDNS 沒有本機（即用 Go 編寫）遞歸解析器，需要用 cgo 連結 libunbound
