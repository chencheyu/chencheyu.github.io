---
publish: true
slug: 6dea1f0e-987d-42d9-ba0f-86e9835a4e9f
tags:
- CS
title: GnuEfi
uuid: e17a6ae3-c318-4f9d-9d32-bcc64808d59a
---
https://wiki.osdev.org/GNU-EFI
https://sourceforge.net/projects/gnu-efi/
官網找不到剩sourceforge可以下載，把EDK2的header檔打包成可以用GCC工具鏈編譯專案。
在Ubuntu 22.04LTS上測試確定Hello World可用。

### 安裝

- 確定GCC工具鏈可用
- 下載並解壓縮
- 切進下載的資料夾

```
make
```

- make install
  如果要改預設安裝路徑，要改Make.defaults中的`PREFIX := /usr/local/gnu-efi` 不然會裝去/usr/local

### 編譯

- 編譯

```
gcc -I/usr/local/gnu-efi/include/efi -fpic -ffreestanding -fno-stack-protector -fno-stack-check -fshort-wchar -mno-red-zone -maccumulate-outgoing-args -c hello.c -o hello.o
```

- Link

```
ld -shared -Bsymbolic -L/usr/local/gnu-efi/lib -T/usr/local/gnu-efi/lib/elf_x86_64_efi.lds /usr/local/gnu-efi/lib/crt0-efi-x86_64.o hello.o -o hello.so -lgnuefi -lefi
```

- 轉換為efi格式

```
objcopy -j .text -j .sdata -j .data -j .dynamic -j .dynsym  -j .rel -j .rela -j .rel.* -j .rela.* -j .reloc --target efi-app-x86_64 --subsystem=10 hello.so hello.efi
```
