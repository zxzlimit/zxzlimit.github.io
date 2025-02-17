---
title: quicker博客一键同步
date: 2025-02-17 16:48:51
tags:
  - quicker
categories: 便利
description: 我搭建了一个博客，但是每次保存的进行同步的时候就很麻烦，于是我设想能不能通过quicker，一键输入多行命令进行我博客更新和同步，答案当是可以的
---
# quicker博客一键同步



首先再到gitbash的位置，因为git一般是用这个，这个也方便嘛，然后，将要执行的命令编写好了

```
 cd /c/Users/zxz/Desktop/test	#进入该文件
 git add .
 git commit -m "s"	#这里的时间可以用一个变量代替
 git push origin dev
```

cmd中就可以像这样执行

```
D:\git\Git\git-bash.exe -c "cd /c/Users/zxz/Desktop/test && git add . && git commit -m 's' && git push origin dev"
```

<img src="https://zxztypora.oss-cn-hangzhou.aliyuncs.com/fpa0imix.4wl.png" alt="fpa0imix.4wl" style="zoom:33%;" />

quicker像这样还能做很多东西，比如说快速运行python代码，还有其他的自行探索

<img src="https://zxztypora.oss-cn-hangzhou.aliyuncs.com/mwo20snb.s4s.png" alt="mwo20snb.s4s" style="zoom: 50%;" /> 

