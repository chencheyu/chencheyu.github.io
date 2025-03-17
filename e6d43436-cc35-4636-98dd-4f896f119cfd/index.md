---
date: 2021-01-07
publish: true
slug: 3aa09ab5-0883-4a07-a924-efe2bb9d6d7d
tags:
- CS/Backend
title: "Hugo \u6559\u5B78"
---
### install

先去[copr](https://copr.fedorainfracloud.org/coprs/daftaupe/hugo/)裝hugo官方的repo

```shell=
yum install hugo
```

應該就有hugo可以用了
2025 Ubuntu 24 Apt 安裝版本為 0.123.7; Githab last is 0.143.1, 有些 theme 可不能用

Hugo is available in three editions: standard, extended, and extended/deploy.
至少要 extended 才有 Webp 及 SASS

### 使用

裝theme

```shell=
git clone https://github.com/hauke96/hugo-theme-hamburg.git themes/hamburg
```

改設定檔

```
baseURL = "http://example.org/"
languageCode = "en-us"
title = "ericchen"
theme = "hamburg"

```

```shell=
hugo new site blog
cd blog
hugo new posts/myfirst.md
hugo                       #生成網頁
hugo server -D
```

myfirst應該會出現在content下面
![](../f99b436e-d882-442f-aa6c-a2bfc2407e25.png)

### [Template lookup order](https://gohugo.io/templates/lookup-order/)

如果要覆蓋 themes 提供的文件，如 `themes/hugo-theme-next/assets/css/_variables/base.scss` 可以用`assets/css/_variables/base.scss` 覆蓋，確定可以覆蓋scss 跟靜態文件，預設 site 根資料夾中沒有 assets 請直接創一個

### [hugo-theme-next](https://github.com/hugo-next/hugo-theme-next/tree/main)

用 [hugo-theme-next-starter](https://github.com/hugo-next/hugo-theme-next-starter) 開始，自己建 site 會 build 不過

### ref

https://coolgood88142.github.io/zh-tw/posts/hugo/
