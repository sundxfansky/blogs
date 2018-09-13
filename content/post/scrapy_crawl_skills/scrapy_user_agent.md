---
title: "使用Middleware设置scrapy的User-Agent代理池"
date: 2018-09-01T00:13:23.221+08:00
lastmod: 2018-09-01T00:13:23.221+08:00
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
使用scrapy爬虫时可能会遇到服务器检测爬虫客户端的headers中user-agent，当被检测到同一个IP地址同一个user-agent有类似爬虫的行为时，服务器会对访问作出一些限制，用来保护正常访问的用户，这无疑对爬虫用户不太友好，本文介绍如何使用user-agent代理池破除这一限制。
<!--more--> 
## DownloaderMiddleware（下载器中间件） 的使用
首先先了解一下scrapy的框架，如图：
![架构图](/image/scrapy_architecture_02.png)
关于详细的解释后面会专门写一个文章来写，在图中蓝色的方块就是middleware，从图中可以看出有两个middleware，分别是spider和Downloader两个，对于Downloaded的middleware，也就是对scrapy的engine发出的request请求，做一个预处理从而发给服务器去请求html。有关更详细的关于DownloaderMiddleware的描述可以[点击官网](https://docs.scrapy.org/en/latest/topics/downloader-middleware.html)查看。

> 下载器中间件是介于Scrapy的request/response处理的钩子框架。 是用于全局修改Scrapy request和response的一个轻量、底层的系统。

要想激活自己的下载器中间件设置需要在`settings.py`文件中设置(取消注释)：
```python
DOWNLOADER_MIDDLEWARES = {
    'myproject.middlewares.CustomDownloaderMiddleware': 543,
}
```
留意官网的说明：

>The `DOWNLOADER_MIDDLEWARES` setting is merged with the `DOWNLOADER_MIDDLEWARES_BASE` setting defined in Scrapy (and not meant to be overridden) and then sorted by order to get the final sorted list of enabled middlewares: the first middleware is the one closer to the engine and the last is the one closer to the downloader. In other words, the `process_request()` method of each middleware will be invoked in increasing middleware order (100, 200, 300, …) and the `process_response()` method of each middleware will be invoked in decreasing order.
>
To decide which order to assign to your middleware see the `DOWNLOADER_MIDDLEWARES_BASE` setting and pick a value according to where you want to insert the middleware. The order does matter because each middleware performs a different action and your middleware could depend on some previous (or subsequent) middleware being applied.
>
If you want to disable a built-in middleware (the ones defined in `DOWNLOADER_MIDDLEWARES_BASE` and enabled by default) you must define it in your project’s `DOWNLOADER_MIDDLEWARES` setting and assign None as its value. For example, if you want to disable the user-agent middleware:
>
```python
DOWNLOADER_MIDDLEWARES = {
    'myproject.middlewares.CustomDownloaderMiddleware': 543,
    'scrapy.downloadermiddlewares.useragent.UserAgentMiddleware': None,
}
```

如果上述的`'scrapy.downloadermiddlewares.useragent.UserAgentMiddleware': None,`命令没有修改的话，很有可能在自己修改了user-agent之后又被默认的middleware改回去，失去了修改的作用。

## 自己定义middleware
```python
from fake_useragent import UserAgent

class RandomUserAgentMiddleware(object):
    def __init__(self, crawler):
        super(RandomUserAgentMiddleware, self).__init__()
        self.ua = UserAgent()
        self.ua_type = crawler.settings.get("USER_AGENT_TYPE", "random")

    @classmethod
    def from_crawler(cls, crawler):
        return cls(crawler)

    def process_request(self, request, spider):
        def get_ua_type():
            return getattr(self.ua, self.ua_type)
        request.headers.setdefault(b'User-Agent', get_ua_type())
        pass
```


使用了python3的[fake_useragent](https://github.com/hellysmile/fake-useragent)库,在终端下输入`pip install fake-userage`安装，按照作者的指示：

>
```python
from fake_useragent import UserAgent
ua = UserAgent()

ua.ie
# Mozilla/5.0 (Windows; U; MSIE 9.0; Windows NT 9.0; en-US);
ua.msie
# Mozilla/5.0 (compatible; MSIE 10.0; Macintosh; Intel Mac OS X 10_7_3; Trident/6.0)'
ua['Internet Explorer']
# Mozilla/5.0 (compatible; MSIE 8.0; Windows NT 6.1; Trident/4.0; GTB7.4; InfoPath.2; SV1; .NET CLR 3.3.69573; WOW64; en-US)
ua.opera
# Opera/9.80 (X11; Linux i686; U; ru) Presto/2.8.131 Version/11.11
ua.chrome
# Mozilla/5.0 (Windows NT 6.1) AppleWebKit/537.2 (KHTML, like Gecko) Chrome/22.0.1216.0 Safari/537.2'
ua.google
# Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_4) AppleWebKit/537.13 (KHTML, like Gecko) Chrome/24.0.1290.1 Safari/537.13
ua['google chrome']
# Mozilla/5.0 (X11; CrOS i686 2268.111.0) AppleWebKit/536.11 (KHTML, like Gecko) Chrome/20.0.1132.57 Safari/536.11
ua.firefox
# Mozilla/5.0 (Windows NT 6.2; Win64; x64; rv:16.0.1) Gecko/20121011 Firefox/16.0.1
ua.ff
# Mozilla/5.0 (X11; Ubuntu; Linux i686; rv:15.0) Gecko/20100101 Firefox/15.0.1
ua.safari
# Mozilla/5.0 (iPad; CPU OS 6_0 like Mac OS X) AppleWebKit/536.26 (KHTML, like Gecko) Version/6.0 Mobile/10A5355d Safari/8536.25
# and the best one, random via real world browser usage statistic
ua.random
```

查看源码后为[json文件](http://d2g6u4gh6d9rq0.cloudfront.net/browsers/fake_useragent_0.1.10.json),作者自己维护，后期可以考虑自己将其下载下来到数据库中，从本地读取，但是仍推荐使用云端方法，因为有原作者在维护

可以在`settings.py`中设置`USER_AGENT_TYPE`类型确定，对于`getattr()`函数，可以参考官方文档的解读：

>getattr(object, name[, default])
    
>Return the value of the named attribute of object. name must be a string. If the string is the name of one of the object’s attributes, the result is the value of that attribute. **For example, getattr(x, 'foobar') is equivalent to x.foobar.** If the named attribute does not exist, default is returned if provided, otherwise AttributeError is raised.

而后`settings.py`中设置为：
```python
DOWNLOADER_MIDDLEWARES = {
    'addyourpath.middlewares.RandomUserAgentMiddleware': 543,
    'scrapy.downloadermiddlewares.useragent.UserAgentMiddleware': None,
}
```
最后就完成了user-agent代理池的设置
关于`settings.py`文件又一个小技巧就是，当一个爬虫项目设置多个爬虫网站的时候，可以在spider目录下自己写爬虫代码的项目文件中，如`news.py`中，在自己的类中加入
```python
custom_settings = {
    #仅作演示
    "COOKIES_ENABLED": True
}
```
对应源码可以查看`scrapy/spiders/__init__.py`中，找到`custom_settings`。
感谢众多大神的开源项目的帮助。