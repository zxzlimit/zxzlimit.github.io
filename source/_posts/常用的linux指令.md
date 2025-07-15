---
title: 常用的linux指令
date: 2025-04-21 16:26:22
tags:
    - linux
categories: 学习
description: 常用的linux指令
---
# 常用的linux指令



## 根据域名获取ip

```
nslookup xc104.zjxc.gov.cn
```

得到：

```
zxz@r9000p:~$ nslookup xc104.zjxc.gov.cn
Server:         10.255.255.254
Address:        10.255.255.254#53

Non-authoritative answer:
Name:   xc104.zjxc.gov.cn
Address: 220.191.226.152
```

结果ip为220.191.226.152



## 获取进程

```
获取所有的进程
ps aux

获取特定的
ps aux | grep python
```



## 获取所有进行的端口

```
sudo ss -tulnp
```



## 杀死端口或进程

```
kill -9 PID
```



## 获取系统架构

```
uname -m
```



## 检查端口是否被占用

```
lsof i ;端口号
```

