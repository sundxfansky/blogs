---
title: "Scrapy爬取图片与记录路径"
date: 2018-09-04T18:33:53.917+08:00
lastmod: 2018-09-04T18:33:53.917+08:00
draft: false
tags: [“scrapy”,"image"]
categories: ["python", "爬虫", "课余"]
author: "Tonser"

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
# comment: false
# toc: false
# reward: false
# mathjax: true
---
我们利用scrapy提供的默认的下载图片的pipline来完成利用scrapy爬取图片在`scrapy.pipelines.images.ImagesPipeline`文件中给出了scrapy默认爬取图片的设置，我们只需进行自己单独的设置：<!--more-->

首先需要设置一下自己的Item，在Item的内容设置一项：
```python
class JobboleArticleItem(scrapy.Item):
    #用于下载的图片链接
    front_image_url = scrapy.Field()
    #储存图片的路径
    front_image_path = scrapy.Field()
```
对于储存图片的路径，需要重写`ImagesPipeline`类下面的`item_completed`函数：
在`pipeline`中设置写好数据传输：
```python
class ArticleImagesPipeline(ImagesPipeline):
    def item_completed(self, results, item, info):
        for flag, value in results:
            image_path = value['path']
        item["front_image_path"] = image_path
        return item
```
在`settings`文件中设置：

```python
IMAGES_URLS_FIELD = "front_image_url"
project_path = os.path.dirname(os.path.abspath(__file__))
IMAGES_STORE = os.path.join(project_path, 'images')
#图片限制大小
# IMAGES_MIN_HEIGHT = 100
# IMAGES_MIN_WIDTH = 100
ITEM_PIPELINES = {
    # 'article_spider.pipelines.ArticleSpiderPipeline': 300,
    'scrapy.pipelines.images.ImagesPipeline': 1,
    'article_spider.pipelines.ArticleImagesPipeline': 2,
    # 'article_spider.pipelines.MysqlTwistedPipeline': 1,
}
```
其中储存文件为根目录下的`image`文件。





