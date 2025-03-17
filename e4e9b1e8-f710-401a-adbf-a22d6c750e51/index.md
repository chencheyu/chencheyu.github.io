---
date: 2024-03-01
publish: true
slug: fb96d03e-2b3e-4ad2-a816-1693984271d8
tags:
- CS/Linux
title: Linux Serial
---
### Serial Device

![](../8db62c45-b49a-4aff-807c-6c9cfc8285fb.png)

#### RS-485

接口洞很多，但只需要兩條線，原則上地線不用接，半雙工

### 指令

原則上 Serial Device 會出現在 `/dev/ttyS[數字]` 路徑上

```bash
setserial -g /dev/ttyS[0123]
```

列出串口晶片名及中斷

```bash
dmesg | grep tty
```

```bash
stty -F /dev/ttyS0 -a
```

顯示該 Serial Device 的連線設定資料，其他應用程式連接時也可能會更改

```bash
cat /dev/ttyS0
```

讀資料，如果串口有吐的話

```bash
stty -F /dev/ttyS0 9600 cs8 -cstopb -parenb
```

set the baud rate to 9600, 8 bits, 1 stop bit, no parity
重啟後會重設

### Ref

[Serial HOWTO](https://tldp.org/HOWTO/Serial-HOWTO.html)

#### 圖片來源

Jona, [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0), via Wikimedia Commons
Mayayu, [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0), via Wikimedia Commons
