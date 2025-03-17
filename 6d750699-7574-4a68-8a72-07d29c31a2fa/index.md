---
date: 2025-03-06
publish: true
slug: 8da02895-31ad-4010-baf2-4c804efc4937
tags:
- CS/Linux
title: System Cell
uuid: d0f2598a-2aab-479d-990d-a23c5e30f3c1
---
## [sched_yield](https://man7.org/linux/man-pages/man2/sched_yield.2.html)

Uinx 下的system cell，把線程重新放進排成器後端，通常為了讓其他線程取得鎖使用

## [mseal syscall](https://blog.trailofbits.com/2024/10/25/a-deep-dive-into-linuxs-new-mseal-syscall/)

```c
int mseal(unsigned long start, size_t len, unsigned long flags)
```

[mseal](https://docs.kernel.org/userspace-api/mseal.html)新 System call 不可撤銷的設定記憶體的 NX (不可執行)或 RX權限
原本在 Chrome OS 上的 system call 移植到 Linux 6.10

> once the mapping is sealed, it will stay in the process’s memory until the process terminates.
> Blocked mm syscall:

> - munmap
> - mmap
> - mremap
> - mprotect and pkey_mprotect
> - some destructive madvise behaviors: MADV_DONTNEED, MADV_FREE, MADV_DONTNEED_LOCKED, MADV_FREE, MADV_DONTFORK, MADV_WIPEONFORK
