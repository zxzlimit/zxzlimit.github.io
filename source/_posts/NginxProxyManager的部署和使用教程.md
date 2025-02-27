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

## 1、修改 Docker 配置（可选）

以下配置会增加一段自定义内网 IPv6 地址，开启容器的 IPv6 功能，以及限制日志文件大小，防止 Docker 日志塞满硬盘（泪的教训）：

```
cat > /etc/docker/daemon.json <<EOF
{
    "log-driver": "json-file",
    "log-opts": {
        "max-size": "20m",
        "max-file": "3"
    },
    "ipv6": true,
    "fixed-cidr-v6": "fd00:dead:beef:c0::/80",
    "experimental":true,
    "ip6tables":true
}
EOF
```

然后重启 Docker 服务：

```
systemctl restart docker
```



## 2、要先安装Docker和Docker Compose才方便安装`nginx-proxy-manage`

安装docker

```
 sudo apt-get update
 sudo apt-get install ./docker-desktop-amd64.deb
```

检查是否安装成功

```
docker -v
```

安装docker Compose

```
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

检查是否安装成功

```
docker-compose --version
```





3、查看端口是否被占用（以 81 为例），输入：

```
lsof -i:81  #查看 81 端口是否被占用，如果被占用，重新自定义一个端口
```

如果啥也没出现，表示端口未被占用，我们可以继续下面的操作了～



## 4、然后创建文件写NGX的配置运行

```
sudo -i

mkdir -p /root/data/docker_data/npm

cd /root/data/docker_data/npm
```

编辑`docker-compose.yml`内容如下：

```
version: '3'
services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    ports:
      - '80:80'  # 保持默认即可，不建议修改左侧的80
      - '81:81'  # 冒号左边可以改成自己服务器未被占用的端口
      - '443:443' # 保持默认即可，不建议修改左侧的443
    volumes:
      - ./data:/data # 冒号左边可以改路径，现在是表示把数据存放在在当前文件夹下的 data 文件夹中
      - ./letsencrypt:/etc/letsencrypt  # 冒号左边可以改路径，现在是表示把数据存放在在当前文件夹下的 letsencrypt 文件夹中

```

然后运行该配置文件，这里的-d表示后台运行

```
cd /root/data/docker_data/npm   # 来到 dockercompose 文件所在的文件夹

docker-compose up -d
```



## 5、`nginx-proxy-manager`控制台默认使用81端口，需要防火墙放行81端口，如果有安全组同样需要放行。

浏览器输入地址：`http://ip:81`进入控制台。

默认管理员用户以及密码如下：

```
Email:    admin@example.com
Password: changeme
```

<img src="https://zxztypora.oss-cn-hangzhou.aliyuncs.com/u43d4pb2.3zi.png" alt="u43d4pb2.3zi" style="zoom: 50%;" /> 