---
title: 服务器使用v2raya来实现科学上网（无UI）
date: 2025-02-17 15:59:42
tags:
 - server
categories: 服务器
description: 服务器有时候下载一些东西的时候遇到墙，这很难受，于是我研究了如何用纯命令行来让服务器翻墙，当然也不能说完全的命令行完成，最好还是通过网页ui来进行的
---
# 服务器使用v2raya来实现科学上网（无UI）

使用v2raya对v2ray核心进行管理，实现在本地电脑配置服务器的代理

1、安装v2raya

在https://github.com/v2rayA/v2rayA/releases下载对应的安装包，将其传入到服务器里面

在通过进行安装

```
sudo apt install /path/download/installer_debian_xxx_vxxx.deb ### 自行替换 deb 包所在的实际路径
```

启动v2raya

```
sudo systemctl start v2raya
```

查看运行状态

```
sudo systemctl status v2raya
```

配置v2raya的.config

```
sudo vim /etc/v2raya/config.json
```

改为

```
{
  "api": {
    "enabled": true,
    "listen": "0.0.0.0",   // 设置为 0.0.0.0 以便通过外部访问
    "port": 2017,           // 默认端口是 2017，如果需要，可以改成其他端口
    "auth": {
      "user": "admin",      // 设置用户名
      "password": "your_password"  // 设置密码
    }
  }
}
```

2、安装v2ray和相关配置

参考网址https://github.com/v2fly/fhs-install-v2ray?tab=readme-ov-file

**安装unzip后面解压要用**

```
sudo apt update
sudo apt install unzip
```

**安裝和更新 V2Ray**

```
 bash <(curl -L https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh)
 
 sudo systemctl start v2ray   # 启动
 
 sudo systemctl status v2ray   #查看状态
```

**安裝最新發行的 geoip.dat 和 geosite.dat**

```
bash <(curl -L https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-dat-release.sh)
```

3、去浏览器输入对应网址进行配置

```
http://<your-server-ip>:2017
```

设置里面这么在保存一下

![r0xqu5lg.vls](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/r0xqu5lg.vls.png)

![bngo51a0.0rb](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/bngo51a0.0rb.png)

4、检查是否成功

```
curl -I https://www.google.com
```

很快能进行结果返回即代表成功