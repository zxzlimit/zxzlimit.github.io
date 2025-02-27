---
title: 服务器配置SyncClipboard
date: 2025-02-26 11:22:15
tags:

  - docker
    categories: 实用
    description: SyncClipboard是一个云剪贴版，可以同步电脑手机平板直接的文字，非常无感，推荐
---

# 服务器配置SyncClipboard

1、创建安装目录
创建一下安装的目录：

```
sudo -i

mkdir -p /root/data/docker_data/syncclipboard

cd /root/data/docker_data/syncclipboard
```

2、接着我们来编辑下docker-compose.yml

```
vim docker-compose.yml

```

编辑配置

```
services:
  syncclipboard-server:
    image: jericx/syncclipboard-server:latest
    container_name: syncclipboard-server
    restart: unless-stopped
    ports:
      - "5133:5033" # 左边的5133可以改成服务器上没有用过的其他端口
    environment:
      - SYNCCLIPBOARD_USERNAME=这里改成你的英文的用户名
      - SYNCCLIPBOARD_PASSWORD=这个改成你的密码
 
 #其中的5133可以改成服务器上没有用过的端口，记得修改自己的用户名和密码，修改完成之后，可以在英文输入法下，按 i 修改，完成之后，按一下 esc，然后 :wq 保存退出。
```

3、查看端口是否被占用
查看端口是否被占用（以 5133 为例），输入：

```
lsof -i:5133  #查看 5133 端口是否被占用，如果被占用，重新自定义一个端口
```

4、启动 syncclipboard

```
cd /root/data/docker_data/syncclipboard

docker compose up -d   # 注意，老版本用户用 docker-compose up -d
```