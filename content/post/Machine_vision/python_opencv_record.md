---
title: "学习opencv过程中python的梳理"
date: 2019-03-08T01:37:53.375+08:00
lastmod: 2019-03-12T17:51:55.459+08:00
draft: false
tags: ["Code","Software Engineering"]
categories: ["Code"]
author: "Tonser"
---
最近有个课程需要用到opencv与python的学习，顺便梳理了一下知识点
<!--more-->


## python 中各种括号的区别

大括号{}，字典，dict

中括号[]，列表，list

小括号()，元组，tuple

## 正则表达式
在正则表达式中使用方法如下
```python
import re
a = 'python sdasd 68126 asd __ sda'
re = re.findall('[这里放需要匹配的字符]{数字，如3,6,9,}',a)
# 上述为贪婪模式
# 返回的a 就是匹配的内容，为list
# 注意贪婪模式！！！！大部分该部分的bug的原因
# python 使用的时贪婪模式，当时用贪婪模式的时候为在大括号后面加个？即可 如
re = re.findall('[这里放需要匹配的字符]{数字，如3,6,9,}?',a)
s
# .	代表任意字符
# |	逻辑或操作符
# [ ]	匹配内部的任一字符或子表达式
# [^]	对字符集和取非
# -	定义一个区间
# \	对下一字符取非（通常是普通变特殊，特殊变普通）
# *	匹配前面的字符或者子表达式0次或多次
# *?	惰性匹配上一个
# +	匹配前一个字符或子表达式一次或多次
# +?	惰性匹配上一个
# ?	匹配前一个字符或子表达式0次或1次重复
# {n}	匹配前一个字符或子表达式
# {m,n}	匹配前一个字符或子表达式至少m次至多n次
# {n,}	匹配前一个字符或者子表达式至少n次
# {n,}?	前一个的惰性匹配
# ^	匹配字符串的开头
# \A	匹配字符串开头
# $	匹配字符串结束
# [\b]	退格字符
# \c	匹配一个控制字符
# \d	匹配任意数字
# \D	匹配数字以外的字符
# \t	匹配制表符
# \w	匹配任意数字字母下划线
# \W	不匹配数字字母下划线

```

## 安装anaconda python opencv中遇到的问题
基本上按照安装 anaconda 基本过程就可以，可以添加好path，也可以后面再加，系统给其添加的path为

```
C:\Users\sundx\Anaconda3;
C:\Users\sundx\Anaconda3\Library\mingw-w64\bin;
C:\Users\sundx\Anaconda3\Library\usr\bin;
C:\Users\sundx\Anaconda3\Library\bin;
C:\Users\sundx\Anaconda3\Scripts;
```
这个后面会用到，在pycharm中设置时，先设置interpreter ，路径为` C:\Users\sundx\Anaconda3\python.exe`

设置完成后会自动读取包含的包。之后python console打开不正常，之后可以在pycharm设置中对python console 中添加`name`为PATH的环境变量，内容为复制上述内容即可。
至此有关python的opencv 与pycharm的配置完成

## python的枚举类
```python
from enum import Enum
class VIP(Enum):
    YELLOW = 1;
    GREEN = 2;


VIP.YELLOW # 获取的就是枚举类本身
VIP.YELLOW.value # 获取值
# 枚举类的特点 就是作为标签，不必了解值为多少，这就是枚举的意义。
# 应当确认大写，规则，不可变，防止重复，很有效，使用字典或正常的类，是可变，而且不防止相同的类型
# 枚举的类型，名字，值，同时可以遍历使用 for 循环
# 可以使用别名 使用相同的值，但是使用遍历 不会显示，会认为是别名
# 软件工程有23种设计模式，其中有单例模式，和枚举类的设计方法很相似
```
## python编程中的闭包加环境变量
```python
def cure():
    # 可以在这里面加入环境变量
    def cue_1()
    print("1")
    return cue_1
    # 这就是一个闭包，闭包=环境变量+函数
    # 闭包内部的函数可以使用 `nonlocal` 关键字来继承或者认为在该闭包内的变量是全局 
```

## 匿名函数(lambda表达式)
使用匿名函数使用lambda 定义即可。

```python
def add(x,y):
    return x+y

f = lambda x,y: x+y
lambda para_lsit: expression
f(2,1)
add(2,1)
#结果相同
```
## 三元表达式
在C/C++中 `x>y?x:y`

在python中 `x if x>y else y`
## 函数式编程
### MAP
**推荐多多使用**

ap是一个类,执行for循环，并注意与lambda表达式结合,精简，优美，可读性高
```python
def square(x):
    return x*x
list_x = [1,2,3,4]
list_y = map(square,list_x)
list_y = map(lambda x: x*x,list_x)
对于多个变量
list_z = map(lambda x,y: x*x+y ,list_x,list_y)
```

### reduce
连续计算，连续调用lambda，递归调入参数
```python
from functools import reduce
list_x = [1,2,3,4]
reduce(lambda x,y:x+y,list_x)
```
### filter
过滤掉不需要的内容
```python
list_x = [1,0,1,0,10,1]
r = filter(lambda x: True if x>0 else False,list_x)
print(list(r))
#结果为1，1，10，1
```

## 装饰器
在使用python中，最多使用的代码的，高级用法就是装饰器。