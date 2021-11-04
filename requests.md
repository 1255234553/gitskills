# requests

## 1.基本使用

### 1.1 文档

[官方文档](http://cn.python-requests.org/zh_CN/latest/)

[快速上手](http://cn.python-requests.org/zh_CN/latest/user/quickstart.html)



### 1.2 安装

`pip install requests`



### 1.3 response的属性及类型

```python
# @File : requests的基本使用
# @Project : python基础

import requests

url = 'http://www.baidu.com'

response = requests.get(url=url)

# 一个类型和六个属性
# Response类型
# print(type(response))

# 设置响应的编码格式
response.encoding = 'utf-8'

# 以字符串的形式来返回网页的源码
print(response.text)

# 返回一个url地址
print(response.url)

# 返回的是二进制的数据
print(response.content)

# 返回响应的状态码
print(response.status_code)

# 返回的是响应头
print(response.headers)
```



## 2. get请求

```python
# @File : request_get请求
# @Project : python基础

# urllib
# (1) 一个类型及六个方法
# (2)get请求
# (3)post请求
# (4)ajax的get请求
# (5)ajax的post请求
# (6)cookie登录
# (7)代理


# requests
# (1)一个类型以及六个属性
# (2)get请求
# (3)post请求
# (4)代理
# (5)cookie  验证码


import requests

url = 'https://www.baidu.com/s?'

headers = {
    'User-Agent' : 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36'
}

data = {
    'wd':'北京'
}

# url 请求资源路径
# params  参数
# kwargs  字典
response = requests.get(url=url,params=data,headers=headers)

content = response.text

print(content)

# 总结
# (1)参数使用params传递
# (2)参数无需urlencode编码
# (3)不需要请求对象的定制
# (4)请求资源路径的?可以加也可以不加
```



## 3. post请求

```python
# @File : requests_post请求
# @Project : python基础

import requests

url = 'https://fanyi.baidu.com/sug'

headers = {
    'User-Agent' : 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36'
}

data = {
    'kw':'eye'
}

# url  请求地址
# data 请求参数
# kwargs  字典
response = requests.post(url=url,data=data,headers=headers)

content = response.text

import json

obj = json.loads(content)
print(obj)

# 总结：
# (1)post请求不需要编解码
# (2)post请求的参数是data
# (3)不需要请求对象的定制
```



## 4. 代理

```python
# @File : requests_解析
# @Project : python基础

import requests

url = 'https://www.baidu.com/s?'

headers = {
    'User-Agent' : 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36'
}

data = {
    'wd':'ip'
}


proxy = {
    'http':'113.254.178.224:8193'
}

response = requests.get(url=url,params=data,headers=headers,proxies=proxy)

content = response.text

with open('daili.html','w',encoding='utf-8')as fp:
    fp.write(content)
```



## 5. cookie登录

```python
# @File : requests_cookie登录
# @Project : python基础

# 通过登录进入到主页面

# 通过找登录接口我们发现  登录的时候需要的参数很多
# __VIEWSTATE: HTqb2gZ7NW+UBfQWu+NZlWd/eV9SSZcUudfmgTjuMG6pnLpoZ2rXPOXIfJXknVlgtFUzhGYBkfAzRndjJCjc3W2DF5ngQLTG8xx3f88JsZsRUN1UH0W9dtys1G0=
# __VIEWSTATEGENERATOR: C93BE1AE
# from: http://so.gushiwen.cn/user/collect.aspx
# email: 595165358@qq.com
# pwd: action
# code: wc0x
# denglu: 登录

# 我们观察到__VIEWSTATE __VIEWSTATEGENERATOR  code是变量

# 难点：(1)__VIEWSTATE __VIEWSTATEGENERATOR
#      我们观察到这两个数据在页面的源码中  所以我们需要获取网页的源码然后进行解析就可以获取了
#      (2)验证码

import requests

# 这是登陆页面的url地址
url = 'https://so.gushiwen.cn/user/login.aspx?from=http://so.gushiwen.cn/user/collect.aspx'

headers = {
    'User-Agent' : 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36'
}

# 获取页面的源码
response = requests.get(url=url,headers=headers)
content = response.text

# 解析页面源码然后获取__VIEWSTATE __VIEWSTATEGENERATOR
from bs4 import BeautifulSoup

soup = BeautifulSoup(content,'lxml')

# 获取__VIEWSTATE
viewstate = soup.select('#__VIEWSTATE')[0].attrs.get('value')

#获取__VIEWSTATEGENERATOR
viewstategenerator = soup.select('#__VIEWSTATEGENERATOR')[0].attrs.get('value')



# 获取验证码图片
code = soup.select('#imgCode')[0].attrs.get('src')
code_url = 'https://so.gushiwen.cn/' + code


# 有坑
# import urllib.request
#
# urllib.request.urlretrieve(url=code_url,filename='code.jgp')
# requests里面有一个方法 session()通过session的返回值就能使请求变成一个对象

session = requests.session()
# 验证码的url的内容
response_code = session.get(code_url)
# 注意此时要使用二进制数据  因为我们要使用的是图片的下载
content_code = response_code.content
# wb的模式就是将二进制数据写入到文件
with open('code.jgp','wb')as fp:
    fp.write(content_code)

# 获取了验证码的图片之后下载到本地然后观察验证码观察之后然后在控制台输入这个验证码就可以将这个值给code的参数就可以登陆了
code_name = input('请输入你的验证码')

# 点击登录
url_post = 'https://so.gushiwen.cn/user/login.aspx?from=http://so.gushiwen.cn/user/collect.aspx'

data_post = {
    '__VIEWSTATE': viewstate,
    '__VIEWSTATEGENERATOR': viewstategenerator,
    'from': 'http://so.gushiwen.cn/user/collect.aspx',
    'email': '595165358@qq.com',
    'pwd': 'action',
    'code': code_name,
    'denglu': '登录',
}

response_post = session.post(url=url,headers=headers,data=data_post)

content_post = response_post.text

with open('gushiwen.html','w',encoding='utf-8')as fp:
    fp.write(content_post)



# 难点
# (1)   隐藏域
# (2)   验证码
```

