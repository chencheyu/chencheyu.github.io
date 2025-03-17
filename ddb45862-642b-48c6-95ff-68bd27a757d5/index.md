---
date: 2024-01-18
publish: true
slug: b964eee5-6b01-4732-ba22-1f822a1dc7c4
tags:
- CS/Linux
title: ELF
uuid: 96b88f59-121b-4ff2-b52e-dbd9fa40dacd
---
## 簡介

> 在 Linux 中，ELF代表可執行和可連結格式。它是可執行檔、目標程式碼、共用程式庫和核心轉儲的標準檔案格式。 Linux 以及其他類 UNIX 系統使用 ELF 作為二進位檔案的主要格式



又名 Object File
[Introduction To ELF In Linux: A Simple Guide To Executable Files](https://ostechnix.com/elf-in-linux/)

### [Exploring object file formats](https://maskray.me/blog/2024-01-14-exploring-object-file-formats)

簡介了可執行檔的歷史及 EIF 格式
a.out 是 Unix 一開始(PDP-11)使用的連結檔格式，原始是 16 位元但可以延展成 32 及 64 位元

## Structure

### Executable Headers (Ehdr)

在檔案開頭由Magic 7f454c 開始

- Class 32bit or 64bit

```c
typedef struct{
  unsigned char	e_ident[EI_NIDENT];	/* Magic number and other info */
  Elf64_Half	e_type;			/* Object file type */
  Elf64_Half	e_machine;		/* Architecture */
  Elf64_Word	e_version;		/* Object file version */
  Elf64_Addr	e_entry;		/* Entry point virtual address */
  Elf64_Off	e_phoff;		/* Program header table file offset */
  Elf64_Off	e_shoff;		/* Section header table file offset */
  Elf64_Word	e_flags;		/* Processor-specific flags */
  Elf64_Half	e_ehsize;		/* ELF header size in bytes */
  Elf64_Half	e_phentsize;		/* Program header table entry size */
  Elf64_Half	e_phnum;		/* Program header table entry count */
  Elf64_Half	e_shentsize;		/* Section header table entry size */
  Elf64_Half	e_shnum;		/* Section header table entry count */
  Elf64_Half	e_shstrndx;		/* Section header string table index */
} Elf64_Ehdr;
```

e_ident

```c

```

### Section Headers (Shdr)

### Program Headers (Phdr)

## Command

### `readelf -h /usr/bin/find`

列出 ELF 標頭資訊

### `readelf -S /usr/bin/find`

List All Section

### `nm hello`

列出定義在 hello 中的 symbol

### `nm -D hello`

List dynamic symbols
