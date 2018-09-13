---
title: "Scrapy爬取数据保存mysql的方法"
date: 2018-08-30T20:24:09.194+08:00
lastmod: 2018-08-30T20:24:09.194+08:00
draft: false
tags: ["mysql", "scrapy"]
categories: ["python", "爬虫", "课余"]
author: "Tonser"

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
# comment: false
# toc: false
# reward: false
# mathjax: true
---

使用scarpy构建自己的爬虫系统非常简单，本文给出了两种在爬取数据后将数据保存到数据库的方法.

<!--more-->

其中分同步和异步两种方法将数据保存到数据库中，数据库使用mysql，笔者均没有对两种情况的传输方法进行测试。

## 版本

python版本：3.6.5

scrapy 1.5.1

mysql 8.0.12


## 使用同步传输

mysql同步传输
```python
import pymysql#python3版本的mysql的python驱动
from twisted.enterprise import adbapi


#同步机制写入mysql
class MysqlPipeline(object):
    def __init__(self):
        #前四个参数分别为数据库的 host user password name 
        self.conn = pymysql.connect('localhost', 'root', 'password', 'database_name', charset='utf8',use_unicode=True)
        self.cursor = self.conn.cursor()

    def process_item(self, item, spider):
        insert_sql = """
            INSERT INTO table_name(name1, name2, name3)
            VALUES (%s, %s, %s)
        """
        self.cursor.execute(insert_sql, (item['name1'], item['name2'], item['name3']))
        self.conn.commit()
```
为同步传输方法，效率较低，对于有一定规模的系统而言不能满足要求

## 使用异步传输
```python
import pymysql#python3版本的mysql的python驱动
from twisted.enterprise import adbapi


class MysqlTwistedPipeline(object):
    def __init__(self, dbpool):
        self.dbpool = dbpool

    @classmethod
    def from_settings(cls, settings):
        dbparms = dict(
            #要在settings文件中给以下四个参数赋值
            host=settings['MYSQL_HOST'],
            user=settings['MYSQL_USER'],
            password=settings['MYSQL_PASSWORD'],
            database=settings['MYSQL_DATABASE_NAME'],
            charset='utf8',
            cursorclass=pymysql.cursors.DictCursor,
            use_unicode=True,

        )

        dbpool = adbapi.ConnectionPool('pymysql', **dbparms)
        return cls(dbpool)

    # 使用twisted 将mysql插入异步执行
    def process_item(self, item, spider):
        query = self.dbpool.runInteraction(self.do_insert, item)
        query.addErrback(self.handle_error, item, spider)  # 处理异常

    # 处理异常
    def handle_error(self, failure, item, spider):
    #在入库调试的时候可以在此处打断点，方便调试
        print(failure)
    #需要自己在item文件中重写get_insert_sql()函数，返回传入的sql语句与参数
    def do_insert(self, cursor, item):
        insert_sql, params = item.get_insert_sql()
        cursor.execute(insert_sql, params)
```
使用异步的方法，效率较高，且可以轻松应对高并发的大规模爬虫程序，需要注意两点
1.需要在`settings.py`中设置好四个参数，如下：
```python
MYSQL_HOST = "localhost"
MYSQL_DATABASE_NAME = "article_spider"
MYSQL_USER = "root"
MYSQL_PASSWORD = "password"
```
2.需要在自己的`items.py`中重写`get_inser_sql()`函数如下：

```python
    def get_insert_sql(self):
        insert_sql = """
                    insert into table_name(title, url)
                    VALUES (%s, %s)
                    ON DUPLICATE KEY UPDATE salary=VALUES(salary)
                """
        params = (self["title"], self["url"])

        return insert_sql, params
```
