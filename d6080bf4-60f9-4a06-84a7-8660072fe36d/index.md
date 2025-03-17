---
date: 2022-11-07
publish: true
slug: e41987f9-9943-4943-b453-2d17675f514a
tags:
- CS/Windows
title: MinGW32
uuid: 938a1624-d8a4-45d5-8c4a-7428802cde46
---
### CreateProcess

```
process_begin: CreateProcess(NULL, /c/MinGW/bin/mingw32-gcc hello.c -o hello.exe, ...) failed.
```

不論/c/MinGW/bin/mingw32-gcc(UNIX PATH) 還是C:\MinGW\bin\mingw32-gcc(Window Path)多不行，需要把/c/MinGW/bin/加入環境變數直接呼叫mingw32-gcc，建議直接改 Makefile

### bash

改環境變數要去Windows進階使用者設定改，export,set多沒用

### Undef

```make
CROSS_PREFIX=mingw32-
CC=$(CROSS_PREFIX)gcc -U _WIN32

all:
	$(CC) hello.c -o hello.exe
```

```c
#include <stdio.h>
int main(){
	printf("Hello World!\n");
	#if defined(_WIN32)
	printf("Defined _WIN32.\n");
	#endif
	return 0;
}
```

```
Hello World!
```

mingw 用 -U 作為旗標確定可以 undefine mingw取消預定義的_WIN32

```make
CROSS_PREFIX=mingw32-
CC=$(CROSS_PREFIX)gcc

all:
	$(CC) hello.c -o hello.exe
```

```c
#include <stdio.h>
#undef _WIN32
int main(){
	printf("Hello World!\n");
	#if defined(_WIN32)
	printf("Defined _WIN32.\n");
	#endif
	return 0;
}
```

```
Hello World!
```

`undef _WIN32 也可以取消預定義的_WIN32`
