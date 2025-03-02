---
title: Nginx Proxy Manager配置SSL
date: 2025-03-02 10:09:50
tags:
  - Nginx Proxy Manager
categories: 服务器
description: Nginx Proxy Manager配置SSL,打开https的443端口啊，血的教训了。
---
# Nginx Proxy Manager配置SSL

这里有两种方式


~血的教训，记得打开443端口啊！！！这是https的端口，md在这里绕了好久啊！！！
还有配置好可能还是有问题，记得清除浏览器缓存或者换个浏览器打开试一试。



泛域名就是*.zxzflask.cn,其实按理说每一个域名下的子域名都应该单独配置一个ssl证书，但那样太麻烦了，于是就给一个域名配置好就行了，其他就是泛域名属于这个域名下的东西，只要给这个域名配置好了，后面的泛域名就一样了。例如dsada.zxzflask.cn ,adad.zxzflask.cn, 主域名就一个zxzflask.cn罢了。下面图片第一个就是属于泛域名。

![qk0evn04.j1x](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/qk0evn04.j1x.png)



## 1、自己申请证书配置

因为免费证书不支持泛域名。就只能一个一个申请了，不过申请也快的。例如文字a.zxzflask.cn。同时dns解析也要打开哈，必须的。

<img src="https://zxztypora.oss-cn-hangzhou.aliyuncs.com/rjbbjyf0.vmj.png" alt="rjbbjyf0.vmj" style="zoom:33%;" /> 

<img src="https://zxztypora.oss-cn-hangzhou.aliyuncs.com/pxeivvto.dkc.png" alt="pxeivvto.dkc" style="zoom:33%;" /> 

然后下载npm的证书文件，解压得到两个文件，一个后缀为.key:一个后缀为.pem的

![yzz1mdy5.a1c](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/yzz1mdy5.a1c.png) 

然后配置Nginx Proxy Manager，选择上传证书文件。

 <img src="https://zxztypora.oss-cn-hangzhou.aliyuncs.com/uql44sng.4hj.png" alt="uql44sng.4hj" style="zoom:33%;" />

<img src="https://zxztypora.oss-cn-hangzhou.aliyuncs.com/kxsex3ut.wnx.png" alt="kxsex3ut.wnx" style="zoom:33%;" /> 

然后在proxy中选择这个就行了

<img src="https://zxztypora.oss-cn-hangzhou.aliyuncs.com/image-20250302095633072.png" alt="image-20250302095633072" style="zoom:33%;" /> 

## 2、使用dns申请证书配置

<img src="https://zxztypora.oss-cn-hangzhou.aliyuncs.com/hpb0zv5p.xgi.png" alt="hpb0zv5p.xgi" style="zoom:50%;" />

![guw5huto.sk1](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/guw5huto.sk1.png)

![tjc0oilm.x4d](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/tjc0oilm.x4d.png)

然后在Nginx Proxy Manager里面的主机配置好了就行了，也简单的。