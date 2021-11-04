# selenium

## 1. selenium

```
1.什么是selenium
	（1）selenium是一个用于Web应用程序测试的工具
	（2）selenium 测试直接运行在浏览器中，就像真正的用户在操作一样
	（3）支持通过各种driver驱动真实浏览器完成测试
	（4）selenium也是支持无界面浏览器操作的
```

```
2.为什么使用selenium
	模拟浏览器功能，自动执行网页中的js代码，实现动态加载
```

```python
# （1）导入selenium
from selenium import webdriver
# （2）创建浏览器操作对象

path = 'chromedriver.exe'

browser = webdriver.Chrome(path)

# （3）访问网站
# url = 'https://www.baidu.com'
#
# browser.get(url)

url = 'https://www.jd.com/'

browser.get(url)


# page_source获取网页源码
content = browser.page_source
print(content)
```

```python
from selenium import webdriver

path = 'chromedriver.exe'
browser = webdriver.Chrome(path)

url = 'https://www.baidu.com'
browser.get(url)

# 元素定位

# 根据id来找到对象
# button = browser.find_element_by_id('su')
# print(button)

# 根据标签属性的属性值来获取对象的
# button = browser.find_element_by_name('wd')
# print(button)

# 根据xpath语句来获取对象
# button = browser.find_elements_by_xpath('//input[@id="su"]')
# print(button)

# 根据标签的名字来获取对象
# button = browser.find_elements_by_tag_name('input')
# print(button)

# 使用的bs4的语法来获取对象
# button = browser.find_elements_by_css_selector('#su')
# print(button)

# button = browser.find_elements_by_link_text('直播')
# print(button)
```

```python
# @File : 访问元素信息与交互
# @Project : python基础

from selenium import webdriver

path = 'chromedriver.exe'
browser = webdriver.Chrome(path)

url = 'http://www.baidu.com'
browser.get(url)

input = browser.find_element_by_id('su')

# 获取标签的属性
print(input.get_attribute('class'))
# 获取标签的名字
print(input.tag_name)

# 获取元素文本
a = browser.find_element_by_link_text('直播')
print(a.text)
```

```python
# @File : selenium交互
# @Project : python基础

from selenium import webdriver

# 创建浏览器对象
path = 'chromedriver.exe'
browser = webdriver.Chrome(path)

# url
url = 'https://www.baidu.com'
browser.get(url)

import time
time.sleep(2)

# 获取文本框的对象
input = browser.find_element_by_id('kw')

# 在文本框中输入周杰伦
input.send_keys('周杰伦')

time.sleep(2)

# 获取百度一下的按钮
button = browser.find_element_by_id('su')

# 点击按钮
button.click()
time.sleep(2)

# 滑到底部
js_bottom = 'document.documentElement.scrollTop=100000'
browser.execute_script(js_bottom)
time.sleep(2)

# 获取下一页的按钮
next = browser.find_element_by_xpath('//a[@class="n"]')

# 点击下一页
next.click()

time.sleep(2)

# 回到上一页
browser.back()

time.sleep(2)

# 回去
browser.forward()

time.sleep(2)

# 退出
browser.quit()
```

## 2. Chrome handless（无界面浏览器）

Chrome-handless模式，Google针对Chrome浏览器59版新增加的一种模式，可以让你不打开UI界面的情况下使用Chrome浏览器，所以运行效果与Chrome保持完美一致。

```python
# 配置
from selenium import webdriver
from selenium.webdriver.chrome.options import Options

chrome_options = Options()
chrome_options.add_argument('--headless')
chrome_options.add_argument('--disable-gpu')

# path是你自己的Chrome浏览器的文件路径、
path = r'C:\Program Files\Google\Chrome\Application\chrome.exe'
chrome_options.binary_location = path

browser = webdriver.Chrome(chrome_options=chrome_options)
```

```python
# 封装
from selenium import webdriver
from selenium.webdriver.chrome.options import Options

def share_browser():
    chrome_options = Options()
    chrome_options.add_argument('--headless')
    chrome_options.add_argument('--disable-gpu')

    # path是你自己的Chrome浏览器的文件路径、
    path = r'C:\Program Files\Google\Chrome\Application\chrome.exe'
    chrome_options.binary_location = path

    browser = webdriver.Chrome(chrome_options=chrome_options)
    return browser

browser = share_browser()

url = 'https://www.baidu.com'

browser.get(url)
```

