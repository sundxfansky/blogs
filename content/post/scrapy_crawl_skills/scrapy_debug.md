---
title: "Scrapy的Debug方法"
date: 2018-09-13T16:14:53.628+08:00
lastmod: 2018-09-15T14:03:43.981+08:00
draft: false
tags: ["scrapy","Debug"]
categories: ["python", "爬虫", "课余"]
author: "Tonser"

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
# comment: false
# toc: false
# reward: false
# mathjax: true
---
在使用scrapy的过程中要注重调试技巧，使用下面的方法可以提升debug的效率：

# 使用main函数调试
Scrapy是一个框架，启动爬虫的时候需要在命令行下启动，输入`scrapy crawl project_name`我们可以写一个函数实现整个过程，用来进行debug非常方便：
<!--more-->
```python
# -*- coding:utf-8 -*-
__author__ = "sundxfansky@sjtu.edu.cn"

from scrapy.cmdline import execute
import sys
import os

#下面的路径可以满足，但是需要重新修改
#sys.path.append("/Users/sundx/Documents/learn_code/article_spider")

#获取当前目录的父目录

sys.path.append(os.path.dirname(os.path.abspath(__file__)))
execute(["scrapy", "crawl", "jobbole"])
```

利用scrapy.cmdline中的execute函数表示执行终端下的命令。
`os.path.abspath(__file__)`表示当前文件的目录。`os.path.dirname(dir)`表示`dir`目录的母目录
`sys.path.append(dir)`表示将当前sys的路径设置在`dir`下，从而可以执行`execute`命令。

# pycharm断点调试
在文件中加入断点时执行debug会有两种方法进行，F6单步调试，与F8进行下一步调试，注意观察debug信息与variables，后期会在本文中加入常见的debug信息错误与对应的错误类型

# 数据库入库之前的调试问题

在数据库入库之前的命令中加入一个断点，便于准确的跟踪数据入库的错误，及时发现。

-------后续再进行补充---------