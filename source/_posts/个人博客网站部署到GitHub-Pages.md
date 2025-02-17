---
title: 个人博客网站部署到GitHub Pages
date: 2025-02-17 15:23:56
tags:
  - Next
categories: 博客
description: 将个人博客网站部署到GitHub Pages，通过git来进行网站更新。
---

# 一、注册GitHub账号

后面要将我们的个人博客网站部署到GitHub Pages上，拥有一个GitHub账户自然就是最基本的前提了。

百度搜索“gitub”，搜索结果如下图所示：

![img](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/1.png)

选择并点击“GitHub Build software better, together.”，或直接访问https://github.com/
进入如下图所示界面：

![img](https://oceanwang.top/personal-website-7/2.png)



- 如果是第一次使用GitHub，点击“Sign up”进行注册；
- 如果以前使用过GitHub，点击“Sign in”登录即可。

# 二、创建部署目录仓库

按照官方说明的使用规则，如果使用GitHub Pages进行网站部署的话，所建仓库必须要取名为“GitHub用户名.github.io”。因为我的GitHub用户名为Napoleon940911，所以我的这个仓库应取名为“Napoleon940911.github.io”。

在GitHub官网（https://github.com/）上成功登录后，找到并点击网页左上方的“New”：

![img](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/3.png)

从而进入如下网页：

![img](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/4.png)

依次：



- 在上图所示的“Repository name”方框中填入仓库名称；
- 勾选“Add a README file”；
- 点击“Create repository”。
  即可完成该仓库的创建（简单起见，其余所有内容均保持默认）。

***注意：一定要勾选“Add a README file”，不然后面会看不到GitHub Pages的域名和部署分支\***

# 三、访问GitHub Pages

该仓库创建成功后，会进入如下图所示网页：

![img](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/5.png)



点击上图中的“Settings”，将所进入的网页滚轮移动至GitHub Pages相关的部分，如下图所示：

![img](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/6.png)

从上图中可以看出，GitHub Pages给我们提供了一个格式为[https://GitHub用户名.github.io](https://xn--github-8h6jw94g4v9a.github.io/) 的免费域名，并且相应的网站是从该仓库的 main 分支构建得到的。



我们直接点击上图中的这个域名，或是将这个域名（https://napoleon940911.github.io/）输入浏览器的地址栏并回车，可以看到如下图所示的界面：

![img](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/7.png)

如果你成功看到上图这样的界面，那么恭喜你已经拥有一个自己专属的网站了！！！



# 四、设置部署仓库和分支

回到我们前面创建的Hexo源码目录，用Notepad++或记事本等文本编辑工具打开根目录下面的 _config.yml 文件，并滚动到文件最后，可以看到如下图所示内容：

![img](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/8.png)



将上图中这部分的内容更改为如下图所示：

![img](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/9.png)



关于上图中“repo”内容的获取，如下图所示：

![img](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/10.png)

依次点击上图中3个圈出的位置，即可将我们需要的信息添加到**剪切板** 里面，直接粘贴到前面提到的 _config.yml 文件中最后的**repo:**后面即可。



关于branch的填写，必须要和https://github.com/Napoleon940911/Napoleon940911.github.io/settings 中GitHub Pages部分指定的**Branch**保持一致。
保存_config.yml文件，并退出。

# 五、生成静态网页文件

在Git Bash窗口中输入如下指令并回车，将Hexo源码目录中已有的源码编译生成为静态网页文件：
hexo generate
该指令执行完成后，如下图所示：

![img](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/11.png)



与此同时，可以看到Hexo源码目录中新增了一个名为db.json的文件，以及一个名为public的文件夹，如下图所示。

![img](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/12.png)



- db.json文件：编译过程中产生的中间文件，不用关心；
- public文件夹：新生成的静态网页文件就存放在这个目录下。

点进public文件夹可以看到：

![img](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/13.png)

这些就是刚刚编译生成的静态网页文件。



# 六、部署到GitHub Pages上

在Git Bash窗口中输入如下指令并回车，将刚刚新生产的静态网页文件推送到GitHub Pages：
hexo deploy
该指令执行完成后，如下图所示：

![img](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/14.png)

上图中最后一行提示 Deploy done，意味着我们部署成功了！



# 七、再次访问GitHub Pages

这时，我们再去访问我们前面得到的 GitHub Pages（https://napoleon940911.github.io/） 。会发现原来几乎空白的网页，已经变成了前面我们在本地通过 [http://localhost:4000](http://localhost:4000/) 所访问到的网页了！如下图所示：

![img](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/15.png)



如果测试发现 GitHub Pages 还是没有任何变化，不要着急，等几分钟之后再次刷新即可。

至此，我们就已经成功将本地的 Hexo 仓库部署到 GitHub 上了。



**更新**

最好设置两个分支，一个管理代码，一个展示网页

代码管理就是和平时的git一样，将写好的代码上传到git进行备份

网页展示的则进入本地项目的文件夹里，通过命令，直接推送过去了，其他不用管了

```
hexo d
```





**一些git的简单命令**

强制推送

```
git add .
git commit -m "Your commit message"
git push --set-upstream git@github.com:zxzlimit/zxzlimit.github.io.git main --force
```

以后要推送的话

```
git push origin main
```



```
本地连接远程
git remote add origin git@github.com:zxzlimit/zxzlimit.github.io.git

本地分支命名
git branch -m master main

查看是否连接远程
git remote -v

推送到远程dev分支下
git push origin dev
```

