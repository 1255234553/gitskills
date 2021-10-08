# 爬百度首页的热搜

```python
import scrapy


class HelloSpider(scrapy.Spider):
    name = 'hello' # 爬虫名字
    allowed_domains = ['www.baidu.com']

    # 爬取百度首页的热搜
    start_urls = ['http://www.baidu.com/']

    def parse(self, response): # 当scrapy自动向start_urls中的每一个url发起请求后，会将响应对象保存在response对象中
        # 代码一般是在parse方法中写
        hots = response.xpath('//ul[@id="hotsearch-content-wrapper"]/li')
        for hot in hots:
            # xpath返回的是一个列表，但这里列表在的每一个元素都是Selector类型的对象

            # extract()可以将Selector对象中data参数对应的字符串提取出来
            # extract()也可以将列表中每一个Selector对象中data参数对应的字符串提取出来
            contents =hot.xpath(' ./a//span//text()').extract()     # 爬取百度热搜
            title ="".join(contents)
            print(title)

```

![结果](C:\Users\lq\Desktop\TBG0(8_UDU~X06CXVIUGV)D.png)

