# Scrapy

## 创建项目

```
scrapy startproject xxx
```

创建一个包含一些内容的目录

```
xxx/
    scrapy.cfg            # deploy configuration file

    xxx/                  # project's Python module, you'll import your code from here
        __init__.py

        items.py          # project items definition file

        middlewares.py    # project middlewares file

        pipelines.py      # project pipelines file

        settings.py       # project settings file

        spiders/          # a directory where you'll later put your spiders
            __init__.py
```

![架构图](C:\Users\lq\Desktop\20200321114058862.png)

![说明](C:\Users\lq\Desktop\cae91728c6303c4c8b5bcb72e25d5ced.jpg)

## Spider

Spiders 是您定义的类，Scrapy 使用它从一个网站（或一组网站）抓取信息。他们必须子类化 [`Spider`](https://docs.scrapy.org/en/latest/topics/spiders.html#scrapy.spiders.Spider)并定义要发出的初始请求，可选择如何跟踪页面中的链接，以及如何解析下载的页面内容以提取数据。

这是一个 Spider 的代码。将其保存在项目目录`xxx/spiders`下命名的`quotes_spider.py`文件中：

```python
import scrapy


class QuotesSpider(scrapy.Spider):
    name = "quotes"

    def start_requests(self):
        urls = [
            'http://quotes.toscrape.com/page/1/',
            'http://quotes.toscrape.com/page/2/',
        ]
        for url in urls:
            yield scrapy.Request(url=url, callback=self.parse)

    def parse(self, response):
        page = response.url.split("/")[-2]
        filename = f'quotes-{page}.html'
        with open(filename, 'wb') as f:
            f.write(response.body)
        self.log(f'Saved file {filename}')
```

 Spider 子类化[`scrapy.Spider`](https://docs.scrapy.org/en/latest/topics/spiders.html#scrapy.spiders.Spider) 并定义了一些属性和方法：

- `name`: 标识蜘蛛。它在一个项目中必须是唯一的，即不能为不同的 Spider 设置相同的名称。

- `start_requests()`: 必须返回一个可迭代的请求（您可以返回一个请求列表或编写一个生成器函数），蜘蛛将从中开始爬行。后续请求将从这些初始请求中依次生成。

- `parse()`: 一个将被调用以处理为每个请求下载的响应的方法。response 参数是一个实例，`TextResponse`它保存页面内容并有更多有用的方法来处理它。

  该`parse()`方法通常解析响应，将抓取的数据提取为 dicts，并找到要遵循的新 URL 并`Request`从中创建新请求 ( )。

## 运行spider

转到最上层目录运行`scrapy crawl quotes`

注意到已经创建了两个新文件：*quotes-1.html*和*quotes-2.html*，其中包含相应 URL 的内容，正如我们的`parse`方法所指示的那样。

## 可用工具命令

`scrapy <command> -h`

### 全局命令

- `startproject`：`scrapy startproject <project_name> [project_dir]`创建项目

- `genspider`：`scrapy genspider [-t template] <name> <domain>` 

  `spiders`如果从项目内部调用，则在当前文件夹或当前项目的文件夹中创建一个新蜘蛛。这个 `<name>` 参数设置为spider的 `name` ，同时 `<domain>` 用于生成 `allowed_domains` 和 `start_urls` 蜘蛛的属性。

- `settings`：`scrapy settings [options]`获取 Scrapy 设置的值。

  如果在项目中使用，它将显示项目设置值，否则它将显示该设置的默认 Scrapy 值。

- `runspider`：`scrapy runspider <spider_file.py>`运行一个包含在python文件中的spider，而不必创建一个项目。

- `shell`：`scrapy shell [url]`为给定的URL（如果给定）启动scrapy shell；如果没有给定URL，则为空。

  支持的选项：

  - `--spider=SPIDER` ：绕过Spider自动检测并强制使用特定Spider
  - `-c code` ：评估shell中的代码，打印结果并退出
  - `--no-redirect` ：不遵循HTTP 3xx重定向（默认为遵循它们）；这只影响在命令行上作为参数传递的URL；一旦进入shell， `fetch(url)` 默认情况下仍将遵循HTTP重定向。

- `fetch`：`scrapy fetch <url>`使用ScrapyDownloader下载给定的URL，并将内容写入标准输出。这个命令的有趣之处在于它获取了蜘蛛如何下载它的页面。

  - 例如，如果蜘蛛 `USER_AGENT` 覆盖用户代理的属性，它将使用该属性。所以这个命令可以用来“查看”蜘蛛如何获取特定的页面。
  - 如果在项目之外使用，则不会应用特定的每蜘蛛行为，它只会使用默认的scrapy下载器设置。

- `view`：`scrapy view <url>`在浏览器中打开给定的URL，因为您的废蜘蛛会“看到”它。有时候蜘蛛看到的页面与普通用户不同，所以这可以用来检查蜘蛛“看到”什么，并确认它是你所期望的。

  支持的选项：

  - `--spider=SPIDER` ：绕过Spider自动检测并强制使用特定Spider
  - `--no-redirect` ：不遵循HTTP 3xx重定向（默认为遵循它们）

- `version`：`scrapy version [-v]`打印残缺版本。如果使用 `-v` 它还打印python、twisted和platform信息，这对bug报告很有用。

### 仅project命令

- `crawl`:`scrapy crawl <spider>`开始爬行
- `check`：`scrapy check [-l] <spider>`运行检查
- `list`：`scrapy list`列出当前项目所有可用的spider
- `edit`：使用中定义的编辑器编辑给定的蜘蛛 `EDITOR` 环境变量或（如果未设置） [`EDITOR`](https://www.osgeo.cn/scrapy/topics/settings.html#std-setting-EDITOR) 设置。
- `parse`：`scrapy parse <url> [options]`获取给定的URL，并使用处理它的spider，使用 `--callback` 选项，或 `parse` 如果没有给出。
- `bench`：`scrapy bench`运行一个快速基准测试。

## 提取数据

使用Scrapy shell:`scrapy shell 'http://quotes.toscrape.com/page/1/'`**(url要在引号中)**

在Windows中使用双引号。

[`shell`](https://docs.scrapy.org/en/latest/topics/commands.html#std-command-shell)也适用于本地文件。如果您想使用网页的本地副本，这会很方便。`shell`了解本地文件的以下语法：

```
# UNIX-style
scrapy shell ./path/to/file.html
scrapy shell ../other/path/to/file.html
scrapy shell /absolute/path/to/file.html

# File URI
scrapy shell file:///absolute/path/to/file.html
```

### scrapy shell

是一个交互式 shell，您可以在其中快速调试抓取代码，而无需运行蜘蛛程序。它旨在用于测试数据提取代码，但您实际上可以使用它来测试任何类型的代码，因为它也是一个常规的 Python shell。

shell 用于测试 XPath 或 CSS 表达式，并查看它们如何工作以及它们从您尝试抓取的网页中提取哪些数据。它允许您在编写蜘蛛程序时以交互方式测试表达式，而无需运行蜘蛛程序来测试每个更改。

## 存储抓取的数据

存储抓取数据的最简单方法是使用`Feed exports`，并使用以下命令：

```
scrapy crawl quotes -O quotes.json
```

这将生成一个`quotes.json`包含所有抓取项目的文件，以JSON序列化。

该`-O`命令行开关覆盖任何现有的文件; `-o`改为使用将新内容附加到任何现有文件。但是，附加到 JSON 文件会使文件内容成为无效的 JSON。附加到文件时，请考虑使用不同的序列化格式，例如[JSON Lines](http://jsonlines.org/)：

```
scrapy crawl quotes -o quotes.jl
```

该`JSONlines`格式是因为它的流状，你可以很容易地追加新的记录，它是有用的。当你运行两次时，它没有同样的 JSON 问题。此外，由于每条记录都是单独的一行，因此您可以处理大文件而不必将所有内容都放入内存中，因此有像[JQ](https://stedolan.github.io/jq)这样的工具可以帮助在命令行中执行此操作。

如果您想对抓取的项目执行更复杂的操作，则可以编写[Item Pipeline](https://docs.scrapy.org/en/latest/topics/item-pipeline.html#topics-item-pipeline)。创建项目时，已为您设置了 Item Pipelines 的占位符文件，格式为 `tutorial/pipelines.py`. 尽管如果您只想存储抓取的项目，则不需要实现任何项目管道。

## settings.py配置文件

- `BOT_NAME `：项目名

- `USER_AGENT`：默认是注释的，这个东西非常重要，如果不写很容易被判断为电脑，简单点洗一个Mozilla/5.0即可
- `ROBOTSTXT_OBEY`：是否遵循机器人协议，默认是true，需要改为false，否则很多东西爬不了
- `CONCURRENT_REQUESTS`：最大并发数，很好理解，就是同时允许开启多少个爬虫线程
- `DOWNLOAD_DELAY`：下载延迟时间，单位是秒，控制爬虫爬取的频率，根据你的项目调整，不要太快也不要太慢，默认是3秒，即爬一个停3秒，设置为1秒性价比较高，如果要爬取的文件较多，写零点几秒也行
- `COOKIES_ENABLED`：是否保存COOKIES，默认关闭，开机可以记录爬取过程中的COKIE，非常好用的一个参数
- `DEFAULT_REQUEST_HEADERS`：默认请求头，上面写了一个USER_AGENT，其实这个东西就是放在请求头里面的，这个东西可以根据你爬取的内容做相应设置。
- `ITEM_PIPELINES`：项目管道，300为优先级，越低越爬取的优先度越高

