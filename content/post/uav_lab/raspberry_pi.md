---
title: "树莓派安装ubuntu-server系统后安装图像化界面的问题"
date: 2018-09-22T21:13:34.586+08:00
lastmod: 2018-09-22T21:13:34.586+08:00
draft: false
tags: ["Raspberry_pi","Debug"]
categories: ["Ubuntu", "UAV_LAB"]
author: "Tonser"

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
# comment: false
# toc: false
# reward: false
# mathjax: true
---
# 树莓派安装Ubuntu系统
直接从ubuntu的官网wiki中下载就好了，注意都是服务器版本的ubuntu，对于树莓派来讲，安装时要求的sd卡品质较好，师兄测试闪迪的效果最好。

# 安装桌面环境
ubuntu在原始状态的源不要更改，在更换为国内源之后都出现了can‘t locate pacakge的结果，最终换回原本的源解决，之后装ROS就很顺畅了。
