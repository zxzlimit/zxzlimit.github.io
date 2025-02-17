---
title: NginxProxyManager的部署和使用教程
date: 2025-02-17 17:07:55
tags:
  - NPM
  - server
categories: 服务器
description: 服务器一般都是需要搞网页的嘛，网页离不开nginx，NPM就是一个webui化管理nginx的工具嘛，会用它了就不需要在nginx的配置文件里面慢慢敲了，很方便。
---


# NginxProxyManager的部署和使用教程

要先安装docker才方便安装`nginx-proxy-manage`

```
mkdir nginx-proxy-manager
cd nginx-proxy-manager
touch docker-compose.yml
```

编辑`docker-compose.yml`内容如下：

```
services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    container_name: nginx-proxy-manager
    restart: unless-stopped
    ports:
    - '80:80'
    - '81:81'
    - '443:443'
    volumes:
    - ./data:/data
    - ./letsencrypt:/etc/letsencrypt
    networks:
    - nginx_network # 加入nginx_network 网络

networks:
nginx_network:
external: true # 声明此网络为外部网络，需确保nginx_network网络已事先创建
```

上面使用了一个nginx_network网络，后续部署所有的服务都可以加入此网络内，在同一网络下的服务不需要对外暴露端口，安全性大大提高。 启动服务前需要手动创建这个网络：

```
docker network create nginx_network
```

查看已创建网络：

```
docker network ls
```

然后启动：

```
docker compose up -d
或者
docker-compose up -d
```

可以使用下面命令查看日志

```
docker ps
docker compose logs app
```

`nginx-proxy-manager`控制台默认使用81端口，需要防火墙放行81端口，如果有安全组同样需要放行。

浏览器输入地址：`http://ip:81`进入控制台。

默认管理员用户以及密码如下：

```
Email:    admin@example.com
Password: changeme
```

<img src="https://zxztypora.oss-cn-hangzhou.aliyuncs.com/u43d4pb2.3zi.png" alt="u43d4pb2.3zi" style="zoom: 50%;" /> 