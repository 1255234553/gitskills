# urllib

## 1.基本使用

```python
# 使用urllib来获取百度首页的源码
import urllib.request


# (1)定义一个url   你要访问的地址
url = 'http://www.baidu.com'

# (2)模拟浏览器向服务器发送请求
response = urllib.request.urlopen(url)

# (3)获取响应中的页面的源码  content 内容
# read方法  返回的是字节形式的二进制数据
# 我们要将二进制的数据转换为字符串
# 二进制--> 字符串    解码  decode('编码的格式')
content = response.read().decode('utf-8')

# (4) 打印内容
print(content)
```

## 2.一个类型和六个方法

 一个类型：HTTPResponse
 六个方法：read readline readlines getcode geturl getheaders

```python
import urllib.request

url = 'http://www.baidu.com'

# 模拟浏览器向服务器发送请求
response = urllib.request.urlopen(url)

# 一个类型和六个方法
# response是HTTPResponse的类型
# print(type(response))

# 按照一个字节一个字节去读
# content = response.read()
#
# print(content)

# 返回多少个字节
# content = response.read(5)
# print(content)

# 读取一行
# content = response.readline()
# print(content)


# content = response.readlines()
# print(content)

# 返回状态码     如果是200那么就证明我们的逻辑没有错
print(response.getcode())

# 返回url地址
print(response.geturl())

# 获取的是一些状态信息
print(response.getheaders())

# 一个类型 HTTPResponse
# 六个方法 read readline readlines getcode geturl getheaders
```

## 3. 下载

```python
import urllib.request

# 下载网页
# url_page = 'http://www.baidu.com'
#
# # url代表的是下载的路径  filename代表文件的名字
# # 在python中可以写变量的名字也可以直接写值
# urllib.request.urlretrieve(url_page,'baidu.html')

# 下载图片
# url_img = 'https://img0.baidu.com/it/u=2845987849,2642460586&fm=26&fmt=auto'
#
# urllib.request.urlretrieve(url_img,'lisa.jpg')

# 下载视频
#.mp4只能在本地看 没有编译器
url_video = 'https://vd4.bdstatic.com/mda-mjbvzk4r35e9g6sw/cae_h264/1634073942797781039/mda-mjbvzk4r35e9g6sw.mp4?v_from_s=hkapp-haokan-shunyi&auth_key=1634213899-0-0-4eb34452012fab5f1d80499bd86c44a5&bcevod_channel=searchbox_feed&pd=1&pt=3&abtest='
urllib.request.urlretrieve(url_video,'guozu.mp4')
```

## 4. 请求对象的定制

UA介绍：User Agent中文名为用户代理，简称UA，它是一个特殊字符串头，使得服务器能够识别客户使用的操作系统及版本、cpu类型、浏览器及版本。浏览器内核、浏览器渲染引擎、浏览器语言、浏览器插件等

语法：`request = urllib.request.Request()`

```python
import urllib.request

url = 'https://www.baidu.com'

# url的组成
# https://www.baidu.com/s?wd=周杰伦

# http/https    www.baidu.com         80/443          s       wd = 周杰伦    #
# 协议            主机                  端口号         路径      参数          锚点
# http 80
# https 443
# mysql 3306
# oracle 1521
# redis 6379
# mongodb 27017

headers = {
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36'
}

# 因为urlopen方法中不能存储字典所有headers不能传递进去
# 请求对象的定制
# 注意 因为参数顺序的问题不能直接写url和headers 中间还有data 所以我们需要关键字传参
request = urllib.request.Request(url=url,headers=headers)


response = urllib.request.urlopen(request)

content = response.read().decode('utf8')

print(content)
```

```python
# Request方法中的参数顺序
class Request:

    def __init__(self, url, data=None, headers={},
```

## 5. 编解码

### 5.1 get请求方式

`urllib.parse.quote()`

```python
# https://www.baidu.com/s?wd=%E5%91%A8%E6%9D%B0%E4%BC%A6
# 需求  获取 https://www.baidu.com/s?wd=周杰伦 的网页源码

import urllib.request
import urllib.parse
url = 'https://www.baidu.com/s?wd='

# 请求对象定制为了解决反爬的第一项手段
headers = {
    'User-Agent' : 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36'
}

# 将周杰伦三个字变成unicode编码的格式
# 我们需要依赖于urllib.parse
name = urllib.parse.quote('周杰伦')

url = url + name



# 请求对象的定制
request = urllib.request.Request(url=url,headers=headers)


# 模拟浏览器向服务器发送请求
response = urllib.request.urlopen(request)

# 获取相应的内容
content = response.read().decode('utf-8')

# 打印数据
print(content)
```



`urllib.parse.urlencode()`

```python
# urlencode应用场景：多个参数的时候

# https://www.baidu.com/s?wd=周杰伦&sex=男
import urllib.parse

data = {
    'wd':'周杰伦',
    'sex':'男',
    'location':'中国台湾省'
}

a = urllib.parse.urlencode(data)
print(a)
```

### 5.2 post请求方式

```python
# post请求方式的参数  必须编码     data = urllib.parse.urlencode(data)
# 参数是放在请求对象定制的方法中    request = urllib.request.Request(url=url,data=data,headers=headers)
# 编码之后  必须调用encode方法    data = urllib.parse.urlencode(data).encode('utf-8')
```

```python
# post请求
import urllib.request
import urllib.parse

url = 'https://fanyi.baidu.com/sug'

headers = {
    'User-Agent' : 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36'
}

data = {
    'kw':'spider',
}

# post请求的参数必须进行编码
data = urllib.parse.urlencode(data).encode('utf-8')

# post的请求的参数是不会拼接在url的后面的   而需要放在请求对象的定制参数中
# post请求的参数必须要进行编码
request = urllib.request.Request(url=url,data=data,headers=headers)

# 模拟浏览器向服务器发送请求
response = urllib.request.urlopen(request)

# 获取响应的数据
content = response.read().decode('utf-8')

# 字符串-->json对象

import json

obj = json.loads(content)
print(obj)
```

```python
import urllib.request
import urllib.parse


url = 'https://fanyi.baidu.com/v2transapi?from=en&to=zh'

headers = {
    'Accept': '*/*',
   # 'Accept-Encoding':' gzip, deflate, br',
    'Accept-Language':' zh-CN,zh;q=0.9',
    'Connection':' keep-alive',
    'Content-Length':' 135',
    'Content-Type':' application/x-www-form-urlencoded; charset=UTF-8',
    'Cookie: BIDUPSID=CB0D780F4BB4AB7EA789C5552D1C4BF3; PSTM=1630668488; BAIDUID=CB0D780F4BB4AB7E7DF34F2BDD210638:FG=1; BDSFRCVID_BFESS=TLtOJeC62iorHy6HMTaot_0fzmKQqtQTH6f3n3ZzcPm80cCUz_7kEG0PSx8g0Kub9Ib-ogKK0mOTHUkF_2uxOjjg8UtVJeC6EG0Ptf8g0f5; H_BDCLCKID_SF_BFESS=tbuO_KIXfC_3fP36qRo25J8ehgT22-usMeIO2hcH0KLKMpTuh4c_yMu7-fQJy5OhMDjib4j2Lxb1MRjvjRoMQl_Oj-JyttIe0GcvLh5TtUJ5JKnTDMRh-RvQjf7yKMnitIj9-pnG2hQrh459XP68bTkA5bjZKxtq3mkjbPbDfn02eCKuDT0WDjQyjH_sJJ0qM4oLXRbObbu_Hn7zepOd5M4pbt-qJtcy-eb8_qnzQnjofMAxbR6Vyp_L5bQnBT5htK_ehtcJLnCWhbOJ3J6rjPPkQN3TQbkO5bRiLR_XWR_VDn3oyT3VXp0n3fRly5jtMgOBBJ0yQ4b4OR5JjxonDh83bG7MJPKtfD7H3KCbfCLWMUK; __yjs_duid=1_6c7a0f63c0a0d4012cbde204a2f9e41b1631265899762; REALTIME_TRANS_SWITCH=1; FANYI_WORD_SWITCH=1; SOUND_SPD_SWITCH=1; HISTORY_SWITCH=1; SOUND_PREFER_SWITCH=1; BDORZ=B490B5EBF6F3CD402E515D22BCDA1598; H_PS_PSSID=; delPer=0; PSINO=1; BAIDUID_BFESS=CB0D780F4BB4AB7E7DF34F2BDD210638':'FG=1; BA_HECTOR=2k848k0l218k002g2m1gmibjd0r; Hm_lvt_64ecd82404c51e03dc91cb9e8c025574=1631844371,1634283119,1634283131; Hm_lpvt_64ecd82404c51e03dc91cb9e8c025574=1634284358; __yjs_st=2_Njc0MzhjYjU1ZTU4ODkyZjE4MTJhOGVmOWRhMWQyZGMzNzc5ZDBkYmYwNTU2YzE3MzdlYmVhN2Y5NmVmN2QyZDgxMmI1MjJjOTc1ZWYxNmUzNWJmMTJmYjNmNWY3NmQzMDE1NWQ0ZWNkMjAyNzU0ZGIxZmZlNmI2NjViZTgyOGViZmJhNmQ2NTdkN2M1YWUwNDhhMTA0YzZiZDdmOTg1MGNiZmFkMmRiMDU4YWJhMDU5ZGZkNTQzZWRhN2Q3MjJjY2FkMTNjMGQ5NWNmMzhmMjA1YzNmYjFiN2ZlZGFiMTg5NGI4ZTViZmViY2ZlNDYwMmFjMTQxNzJkODE4MWJiMl83X2M5MzYwYWZj; ab_sr=1.0.1_YjAyN2EyMTNhOWI5NmZmNmUxMWQ2ODc1ZDE4MDI5NzVmZDZhYmM3YmFhMWVhMmE4ZGU4N2FmNjVlNzExNTlhNjFiMWNiMGFkNWY4MWMxNTBmM2FkZDc1ZTU2NmVhYzQ0MDJmOWY1NDBhNDNiMjg1OTgwNGEzNzgyMWQ4NmE5NTQwOTIzYmE1YmM4MjVlOWRkMjlmYjZiNzQ2NmNjZmVkZA==',
    'Host':' fanyi.baidu.com',
    'Origin: https':'//fanyi.baidu.com',
    'Referer: https':'//fanyi.baidu.com/?',
    'sec-ch-ua':' "Chromium";v="94", "Google Chrome";v="94", ";Not A Brand";v="99"',
    'sec-ch-ua-mobile':' ?0',
    'sec-ch-ua-platform':' "Windows"',
    'Sec-Fetch-Dest':' empty',
    'Sec-Fetch-Mode':' cors',
    'Sec-Fetch-Site':' same-origin',
    'User-Agent':' Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36',
    'X-Requested-With':' XMLHttpRequest',
}

data = {
    'from': 'en',
    'to': 'zh',
    'query': 'love',
    'transtype': 'realtime',
    'simple_means_flag': '3',
    'sign': '198772.518981',
    'token': '5d52f67ae2a39f4778e202cda9e983a7',
    'domain': 'common'
}

# post请求的参数  必须进行编码  并且要调用encode编码
data = urllib.parse.urlencode(data).encode('utf-8')

# 请求对象的定制
request = urllib.request.Request(url=url,data=data,headers=headers)

# 模拟浏览器向服务器发送请求
response = urllib.request.urlopen(request)

# 获取相应的数据
content = response.read().decode('utf-8')


import json

obj = json.loads(content)
print(obj)
```



## 6. ajax的get请求

```python
# get请求
# 获取豆瓣电影的第一页的数据 并且保存起来
import urllib.request

url = 'https://movie.douban.com/j/chart/top_list?type=5&interval_id=100:90&action=&start=0&limit=20'

headers = {
    'User-Agent' : 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36'
}

# （1）请求对象的定制
request = urllib.request.Request(url=url,headers=headers)

# (2) 获取响应的数据
response = urllib.request.urlopen(request)
content = response.read().decode('utf-8')

print(content)

# (3) 数据下载到本地
# open方法默认情况下使用的是gbk的编码     如果我们想要保存汉字  那么需要在open方法中指定编码格式为utf-8
# encoding='utf-8'

# fp = open('douban.json','w',encoding='utf-8')
# fp.write(content)

with open('douban1.json','w',encoding='utf-8')as fp:
    fp.write(content)
```

```python
# https://movie.douban.com/j/chart/top_list?type=5&interval_id=100:90&action=&
# start=0&limit=20

# https://movie.douban.com/j/chart/top_list?type=5&interval_id=100:90&action=&
# start=20&limit=20

# https://movie.douban.com/j/chart/top_list?type=5&interval_id=100:90&action=&
# start=40&limit=20

# https://movie.douban.com/j/chart/top_list?type=5&interval_id=100:90&action=&
# start=60&limit=20

# page      1  2  3  4
# start     0 20 40 60

# start (page - 1)*20

# 下载豆瓣电影前十页的数据
# （1） 请求对象定制
# （2） 获取响应的数据
# （3） 下载数据

import urllib.parse
import urllib.request

def creat_request(page):
    base_url = 'https://movie.douban.com/j/chart/top_list?type=5&interval_id=100:90&action=&'

    data = {
        'start':(page - 1)*20,
        'limit':20
    }

    data = urllib.parse.urlencode(data)

    url = base_url + data

    headers = {
    'User-Agent' : 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36'
}

    request = urllib.request.Request(url=url,headers=headers)
    return request

def get_content(request):
    response = urllib.request.urlopen(request)
    content = response.read().decode('utf-8')
    return content
def down_load(page,content):
    with open('douban_' + str(page) + '.json','w',encoding='utf-8')as fp:
        fp.write(content)

# 程序的入口
if __name__ == '__main__':
    start_page = int(input('请输入起始的页码'))
    end_page = int(input('请输入结束的页码'))

    for page in range(start_page,end_page+1):
#        每一页都有自己的请求对象的定制
        request = creat_request(page)
#       获取响应的数据
        content = get_content(request)
#       下载
        down_load(page,content)
```



## 7. ajax的post请求

```python
# 1页
# http://www.kfc.com.cn/kfccda/ashx/GetStoreList.ashx?op=cname
# cname: 北京
# pid:
# pageIndex: 1
# pageSize: 10


# 2页
# http://www.kfc.com.cn/kfccda/ashx/GetStoreList.ashx?op=cname
# post
# cname: 北京
# pid:
# pageIndex: 2
# pageSize: 10

import urllib.request
import urllib.parse

# base_url = 'http://www.kfc.com.cn/kfccda/ashx/GetStoreList.ashx?op=cname'

def creat_request(page):
    base_url = 'http://www.kfc.com.cn/kfccda/ashx/GetStoreList.ashx?op=cname'

    data = {
        'cname': '北京',
        'pid':'',
        'pageIndex': page,
        'pageSize': '10'
    }
    data = urllib.parse.urlencode(data).encode('utf-8')

    headers = {
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36'
    }


    request = urllib.request.Request(url=base_url,headers=headers,data=data)

    return request
def get_content(request):
    response = urllib.request.urlopen(request)
    content = response.read().decode('utf-8')
    return content

def down_load(page,content):
    with open('kfc_' + str(page) +'.json','w',encoding='utf-8')as fp:
        fp.write(content)


if __name__ == '__main__':
    start_page = int(input('请输入起始页码'))
    end_page = int(input('请输入结束页码'))

    for page in range(start_page,end_page+1):
        # 请求对象的定制
        request = creat_request(page)
        # 获取网页的源码
        content = get_content(request)
        # 下载
        down_load(page,content)
```



## 8. URLError\HTTPError

1. HTTPError类是URLError的子类
2. 导入的包urllib.error.HTTPError         urllib.error.URLError
3. http错误：http错误是针对浏览器无法连接到服务器而增加出来的错误提示。引导并告诉浏览者该页是哪里出了问题。
4. 通过urllib发送请求的时候，有可能会发生失败，这个时候如果想让你的代码更加健壮，可以通过try-except进行捕获异常，异常有两类，URLError\HTTPError

```python
import urllib.request
import urllib.error

# url = 'https://blog.csdn.net/sulixu/article/details/119818949'

url = 'http:www.doudan1111.com'

headers = {
    'User-Agent' : 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36'
}
try:
    request = urllib.request.Request(url=url, headers=headers)

    response = urllib.request.urlopen(request)

    content = response.read().decode('utf-8')

    print(content)
except urllib.error.HTTPError:
    print('系统正在升级。。。')
except urllib.error.URLError:
    print('系统真在升级。。。')
```



## 9. cookie登录

```python
# 适用的场景：数据采集的时候 需要绕过登录  然后进入某个页面
# 个人信息页面是utf-8  但是还报错了编码错误  因为没有进入到个人信息页面   而是跳转到了登陆页面
# 那么登录页面不是utf-8 所以报错

# 什么情况下访问不成功
# 因为请求头的信息不够    所有访问不成功
import urllib.request

url = 'https://weibo.cn/6426593421/info'

headers = {
#   ':authority':' weibo.cn',
#   ':method':' GET',
#   ':path':' /6426593421/info',
#   ':scheme':' https',
    'accept':' text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9',
#    'accept-encoding':' gzip, deflate, br',
    'accept-language':' zh-CN,zh;q=0.9',
    'cache-control':' max-age=0',
#   cookie中携带着你的登录信息    如果有登录之后的cookie  那么我们就可以携带cookie进入任何页面
    'cookie':' _T_WM=4979d33295d16f344f9fd0311c443633; SUB=_2A25Matc5DeRhGeBK6VQU-S3IyT2IHXVvlPlxrDV6PUJbktCOLUzjkW1NR8O-SSjurjTrRmcmYm3PvTx2oCNYDlrb; SUBP=0033WrSXqPxfM725Ws9jqgMF55529P9D9WFPEJTAXD-sAn1sI433oIv55NHD95QcShzcSK.0ShzpWs4DqcjSi--ci-z0i-27BgpLw5tt; SSOLoginState=1634641770',
#   referer    判断当前路径是不是由上一个路径进来的   一般情况下是做图片防盗链
    'referer: https':'//weibo.cn/',
    'sec-ch-ua':' "Chromium";v="94", "Google Chrome";v="94", ";Not A Brand";v="99"',
    'sec-ch-ua-mobile':' ?0',
    'sec-ch-ua-platform':' "Windows"',
    'sec-fetch-dest':' document',
    'sec-fetch-mode':' navigate',
    'sec-fetch-site':' same-origin',
    'sec-fetch-user':' ?1',
    'upgrade-insecure-requests':' 1',
    'user-agent':' Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36',
}
# 请求对象的定制
request = urllib.request.Request(url=url,headers=headers)
# 模拟服务器向服务器发送请求
response = urllib.request.urlopen(request)
# 获取响应的数据
content = response.read().decode('utf-8')

# 将数据保存到本地
with open('weibo.html','w',encoding='utf-8')as fp:
    fp.write(content)
```



## 10. Handler处理器

```python
# 需求：使用handler来访问百度  获取网页源码

import urllib.request

url = 'http://www.baidu.com'

headers = {
    'User-Agent' : 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36'
}

request = urllib.request.Request(url=url,headers=headers)

# handler   build_opener    open

# （1）获取handler对象
handler = urllib.request.HTTPHandler()

# （2）获取opener对象
opener = urllib.request.build_opener(handler)

# （3）调用open方法
response = opener.open(request)

content = response.read().decode('utf-8')

print(content)
```

## 11. 代理服务器

代理的常用功能：

1. 突破自身IP访问限制，访问国外站点
2. 访问一些单位或团体内部资源
3. 提高访问速度（通常代理服务器都设置一个较大的硬盘缓冲区，当有外界的信息通过时，同时也将其保存到缓冲区中，当其他用户再访问相同的信息时，则直接由缓冲区中取出信息，传给用户，以提高访问速度。）
4. 隐藏真实IP（上网者也可以通过这种方式隐藏自己的IP免受攻击）

代码配置代理

- 创建Request对象
- 创建ProxyHandler对象
- 用handler对象创建opener对象
- 使用opener.open函数发送请求

```python
import urllib.request

url = 'https://www.baidu.com/s?wd=ip'

headers = {
    'User-Agent' : 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36'
}

# 请求对象的定制
request = urllib.request.Request(url=url,headers=headers)

# 模拟浏览器访问服务器
# response = urllib.request.urlopen(request)

proxies = {
    # 代理ip
    'http':'202.102.86.228:8080'
}

# handler  build_opener  open
handler = urllib.request.ProxyHandler(proxies = proxies)

opener = urllib.request.build_opener(handler)

response = opener.open(request)
# 获取响应的信息
content = response.read().decode('utf-8')

# 保存
with open('daili.html','w',encoding='utf-8')as fp:
    fp.write(content)
```



## 12. 代理池

```python
import urllib.request
proxies_pool = [
    {'http':'118.24.219.151:16817'},
    {'http':'118.24.219.151:16817'},
]

import random

proxies = random.choice(proxies_pool)

url = 'https://www.baidu.com/s?wd=ip'

headers = {
    'User-Agent' : 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36'
}

request = urllib.request.Request(url=url,headers=headers)

handler = urllib.request.ProxyHandler(proxies=proxies)

opener = urllib.request.build_opener(handler)

response = opener.open(request)

content = response.read().decode('utf-8')

with open('daili.html','w',encoding='utf-8')as fp:
    fp.write(content)
```

