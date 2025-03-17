---
date: 2024-02-02
publish: true
slug: 6bb4502b-79a1-44b4-a932-0e2e4670ec1b
tags:
- CS/Backend
title: Docker.md
---
## Install

```bash
apt install -y docker.io
apt install -y docker-compose
```

官網會要你用 docker 自己的 apt 但 debian 12 的官方庫有包

## Build

注意補充參數位子不可以移動

## Run

```bash
docker run -d --name web --net=host nginx
```

啟動 docker 並放於背景執行
建議 network 用 host mode 避免預設的 bridge mode 需要 server 聽在 0.0.0.0

```bash
-p 8888:8000
```

bridge mode 時做 port 映射(Host:Container)

```bash
docker attach web
```

進入 web Container 的 shell

```bash
docker exec web ps
```

在 web Container 的 shell 執行 ps

```
docker logs web
```

web Container 的 log

## Image

```bash
docker image [補充參數] ls 
```

列出所有 build 好的 image

## Container

```bash
docker ps
docker container ls
```

列出執行中的 Container

```bash
docker ps -a
docker container -a ls
```

列出所有的 Container

```bash
docker container prune
```

清理所有停止的 container

## 移除所有沒用到的 Docker 物件

```bash
docker system prune -a
```

## Image

### [Kasm Workspaces](https://www.kasmweb.com/images)

提供有圖形化介面的 Docker Image(需用 KasmVNC 連線)
[Default Docker Image](https://kasmweb.com/docs/latest/guide/custom_images.html)
`docker run --rm  -it --shm-size=512m -p 6901:6901 -e VNC_PW=password kasmweb/firefox:dev`
`https://127.0.0.1:6901` 連線 Kasm Docker Image 預設需要 `https`
在瀏覽器中用 User : kasm_user，Password: password 登入
