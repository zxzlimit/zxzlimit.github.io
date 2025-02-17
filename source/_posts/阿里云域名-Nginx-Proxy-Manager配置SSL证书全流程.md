---
title: 阿里云域名+Nginx Proxy Manager配置SSL证书全流程
date: 2025-02-17 17:10:31
tags:
  - NPM
categories: 服务器
description: 之前讲过了NPM的安装，现在详细说一下它是怎么配置的，以及一些服务器的基本东西，域名啊，ssl证书啊，dns云解析啊这些，还有国内域名一般都要备案，好麻烦的说啊。
---
# 阿里云域名+Nginx Proxy Manager配置SSL证书全流程



域名就是像wwwbaidu.com这样的东西嘛，其实就是把ip地址隐藏起来，将一个ip加端口给隐藏起来，通过域名访问网站嘛

ssl就是https，更加安全，没有ssl证书只能是http，不太安全

dns云解析，这个就是把域名解析到ip嘛

其实配置这一步就是把ip加端口关联到一个域名。一般前端也好，后端也好，运行都是一个ip加一个端口号的嘛，这样不太好看也暴露了服务器，所以配置一下好一些嘛。



买完域名记得备案，然后是搞ssl证书

下面直接开始操作

注意一点![hq2tyc45.sm4](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/hq2tyc45.sm4.png)

它的domain names对应![e1sp0fla.25i](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/e1sp0fla.25i.png)

#### 阿里云DNS API的获取

##### 创建子账号

前往：https://ram.console.aliyun.com 申请子账号。

![qjsdsrul.e2d](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/qjsdsrul.e2d.png)

名字任意命名，下面勾上：使用永久 AccessKey 访问 [![5fn4elbs.rug](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/5fn4elbs.rug.png)](https://img.idev.ink/2024/12/11/AA9D2F2E-5AD5-4CD2-8754-345E8A22F603.png?size=large)

然后确定

[![j1ixwkc4.ego](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/j1ixwkc4.ego.png)](https://img.idev.ink/2024/12/11/5ADB7A45-10FC-4758-A881-7FAF089AE82D.png?size=large)

把AccessKey ID和Secret都复制下来备用。

##### 子账号授权

点击授权，新增授权： [![5jauoqzb.b1a](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/5jauoqzb.b1a.png)](https://img.idev.ink/2024/12/11/F15DAC2A-5100-473D-9EFA-1CEDDB8E8C7D.png?size=large)

勾选刚才新建的用户，授予两个权限：`AliyunHTTPDNSFullAccess` `AliyunDNSFullAccess`

[![b32wkgiy.wnp](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/b32wkgiy.wnp.png)](https://img.idev.ink/2024/12/11/E085DAAF-9264-4AF1-A1CC-3A35226E537D.png?size=large)

然后确定，aliyun DNS API 获取完毕。

#### 使用 nginx proxy manager 使用阿里云域名为网站部署证书

登录nginx proxy manager 控制台 点击`SSL Certificates`

[![px32tmee.hc0](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/px32tmee.hc0.png)](https://img.idev.ink/2024/12/11/B2F1212A-B64E-40B9-999B-01B5E74261EF.png?size=large)

点击 Add SSL Certificate

[![xi33spac.5hg](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/xi33spac.5hg.png)](https://img.idev.ink/2024/12/11/4C741D10-A009-4C68-AA5A-1F01C11B89BB.png?size=large)

如图所示我设置了一个通配符证书，DNS服务商选阿里云，把下面的API ID和值替换成实际值，点save。 [![fan5whop.dnz](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/fan5whop.dnz.png)](https://img.idev.ink/2024/12/11/2E53D4D0-6AF6-4D4F-A760-FBF0CC40B411.png?size=large)

成功后如图所示： [![image-20250215153255305](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/image-20250215153255305.png)](https://img.idev.ink/2024/12/11/6FA23FE0-008C-444C-9A65-0706DF79EC46.png?size=large)

在部署的其他服务中就可以直接使用了

