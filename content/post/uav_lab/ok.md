---
title: "1111111111111111-test"
date: 2018-12-09T16:30:37.836+08:00
lastmod: 2018-12-09T16:30:37.836+08:00
draft: false
tags: ["Blog","Hugo"]
categories: ["Hugo", "UAV_LAB"]
author: "Tonser"

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
# comment: false
# toc: false
# reward: false
# mathjax: true
---

# 有关本博客的部署
Hugo+jane主题在github上部署，并启用私人域名
有段时间没弄了，今天正好有个下午空闲，更新一下博客，顺便重新部署一下，理清一下思路
<!--more-->

## github
本博客使用github的博客部署系统，有300m的免费空间，一般情况下使用是足够了。
## hugo 框架
使用的框架是hugo，基于go语言的最快的静态网页框架，比其他的网页编译要快很多，而且编写的时候支持本地实时的查看，用起来就很方便
使用的语言是GO语言，google 开发的据说是性能最好的服务器语言
## 初始化
建站过程参考[Hugo-them-jane](https://github.com/xianmin/hugo-theme-jane/blob/master/README-zh.md)
有些内容需要注意：

* hugo的使用方法是hugo server 会在本地生成 `localhost:1313`的实时网址，在建站的过程中可以自己查看效果
* hugo生成的静态网站放在`public`目录中
* Github的建站方法是建立一个仓库，名字为`yourname.github.io`这样会自动生成自己的page，需要把自己的pubic文件与其同步。
* 可以先删除pubic 文件，然后在命令行下输入`git remote add origin your/git/address.git`
* 最后在命令行下重新生成网站`hugo` 将public下的文件push到自己远程仓库

## 绑定自己的域名
可以在public，下面自己新建一个CNAME文件，内部填写自己的域名，在hugo的主题设置里面也需要填写好自己的域名，同时需要在域名商处解析域名，同样使用CNAME
可以参考[域名解析](https://blog.csdn.net/kesixin/article/details/78015934)
我是用的是腾讯云的免费解析如图
<center>![云解析](/image/解析.jpg)</center>

# 彩蛋-交大初雪
2018年12月8日 交大初雪-朋友圈最佳
<center><video id="media" src="/video/sjtu_snow.mp4" controls width="720px" heigt="408px"></video></center>

# 使用脚本一键发布
在完成上述过程后（主要是public的文件夹需要自己设置一下），可以使用一键脚本发布，十分方便


```bash
#!/bin/bash

echo -e "\033[0;32mDeploying updates to GitHub...\033[0m"

# Build the project.
hugo # if using a theme, replace with `hugo -t <YOURTHEME>`

git add .

# Commit changes.
msg="update hugo file  `date`"

if [ $# -eq 1 ]
  then msg="$1"
fi
git commit -m "$msg"

# Push source and build repos.
git push origin master

# Go To Public folder
cd public
# Add changes to git.
git add .

# Commit changes.
msg="update blog web `date`"
if [ $# -eq 1 ]
  then msg="$1"
fi
git commit -m "$msg"

# Push source and build repos.
git push origin master

# Come Back up to the Project Root
cd ..
```
