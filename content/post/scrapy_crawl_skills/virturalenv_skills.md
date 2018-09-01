---
title: "Mac下使用virtualenv搭建python的虚拟环境"
date: 2018-09-01T23:33:21.513+08:00
lastmod: 2018-09-01T23:33:21.513+08:00
draft: false
tags: [“scrapy”]
categories: ["python"]
author: "Tonser"

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
# comment: false
# toc: false
# reward: false
# mathjax: true
---
使用虚拟环境的好处是不会影响系统的环境，可以每开发一个python项目就使用一个虚拟环境，方便管理包，也避免了无用的包。
<!--more-->

## 安装
建议安装 virtualenv与virtualenvwrapper
Virtaulenvwrapper是virtualenv的扩展包，可以更方便地新增，删除，复制，切换虚拟环境。
终端下安装方法：
```
sudo  pip install virtualenv
sudo pip install virtualenvwrapper

```
而后可以配置`virtualenvwrapper`：
下面是安装的虚拟环境的位置:

```
export WORKON_HOME='~/to/your/path'
source /usr/local/bin/virtualenvwrapper.sh
```
将其写入终端的配置文件中,例如如果使用bash，则添加到`~/.bashrc`中；如果使用zsh，则添加到`~/.zshrc`中,或者常用的用户配置文件`~/.bash_profile`.
之后需要source一下生效：
source `~/.bash_profile`

使用方法：
```
查看帮助：virtualenvwrapper --help 
创建基本环境：mkvirtualenv [环境名]
删除环境：rmvirtualenv [环境名]
激活环境：workon [环境名]
退出环境：deactivate
列出所有环境：workon或者lsvirtualenv -b
安装指定版本的python 环境：mkvirtualenv -p python3 artical_spider
```
之后在该环境下安装使用包不会影响系统python或者其他python环境的包，非常方便。

在scrapy开发的时候可以使用这种方法，在pycharm的设置中需要在如图设置：
![pycharm设置](/image/pycharm_settings.png)

