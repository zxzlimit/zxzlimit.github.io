---
title: 电脑SMB连接打印机-直接打印机扫描文件传输到电脑上
date: 2025-02-18 19:34:35
tags:
  - 打印机
categories: 学习
description: 为了不每次去扫描都带一个u盘，插拔插拔的，烦死了，所以研究了一下SMB打印机传输文件到电脑，直接打印机扫描，文件就直接到电脑了
---
# 电脑SMB连接打印机-直接打印机扫描文件传输到电脑上

1、创建一个共享文件

![image-20241209193034235](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/image-20241209193034235.png)

2、共享的相关设置

![image-20241209193100350](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/image-20241209193100350.png)

![image-20241209193127090](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/image-20241209193127090.png)

![image-20241209193152143](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/image-20241209193152143.png)

![image-20241209193218642](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/image-20241209193218642.png)

![image-20241209193229896](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/image-20241209193229896.png)

还有个设置，打开触控面板里面的程序设置

![image-20241209193402217](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/image-20241209193402217.png)

然后就是访问打印机的ip地址了。直接浏览器输入打印机ip地址

![image-20241209193514187](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/image-20241209193514187.png)

然后找到通讯录

设置SMB功能，然后注册

![image-20241209193743809](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/image-20241209193743809.png)

然后确定，然后就配置好了。



总结一下，首先创建一个共享文件，然后配置共享文件的权限，有三步

![image-20241209193903027](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/image-20241209193903027.png)

在然后是计算机程序里面的SMB打开。好了，剩下就是连接打印机ip在上面的通讯录里面添加自己的信息了。具体上面已经写好了，不在复述。

