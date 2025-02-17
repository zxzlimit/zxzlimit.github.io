---
title: Hexo个人博客搭建
date: 2025-02-16 14:45:29
tags:
  - Next
categories: 博客
description: Hexo个人博客搭建及一些基础的命令
---
# hexo搭建个人博客

## 本地搭建

1、先安环境，查看是否安装

检查git是否安装

```
git version
```

检查node是否安装

```
npm -v
```

2、本地搭建

安装hexo脚手架

```
npm install -g hexo-cli
```

进入指定文件

```
cd  /c/Users/zxz/Desktop
```

初始化一个hexo项目在该文件夹下，文件名为test

```
hexo init test
```

如果安装不全，则进入test文件

```
cd test
npm install
```

生成对应文件

```
hexo g
```

<img src="https://zxztypora.oss-cn-hangzhou.aliyuncs.com/cypa2a31.va3.png" alt="cypa2a31.va3" style="zoom: 50%;" />  

启动服务

```
hexo s
```



## 一些常用的hexo命令

```
$ hexo new "My New Post"	#生成新的post文章
$ hexo s	#启动服务
$ hexo g	#更新文件
```

