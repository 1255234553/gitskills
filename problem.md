# 问题

在爬取百度翻译的时候爬取失败出现了

是因为网站的反爬

{'errno': 997, 'errmsg': '未知错误', 'query': 'love', 'from': 'en', 'to': 'zh', 'error': 997}

代码如下：

```python
import urllib.request
import urllib.parse

url = 'https://fanyi.baidu.com/v2transapi?from=en&to=zh'
headers = {
    'User-Agent' : 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36'
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





爬取百度翻译详细翻译时出现错误

已解决：由于使用了编辑器editplus给headers文件加引号时出现了问题，修改后爬取成功

 ![error](https://github.com/1255234553/skills/blob/main/error.png)

代码如下：

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
    'Cookie':' BIDUPSID=CB0D780F4BB4AB7EA789C5552D1C4BF3; PSTM=1630668488; BAIDUID=CB0D780F4BB4AB7E7DF34F2BDD210638:FG=1; BDSFRCVID_BFESS=TLtOJeC62iorHy6HMTaot_0fzmKQqtQTH6f3n3ZzcPm80cCUz_7kEG0PSx8g0Kub9Ib-ogKK0mOTHUkF_2uxOjjg8UtVJeC6EG0Ptf8g0f5; H_BDCLCKID_SF_BFESS=tbuO_KIXfC_3fP36qRo25J8ehgT22-usMeIO2hcH0KLKMpTuh4c_yMu7-fQJy5OhMDjib4j2Lxb1MRjvjRoMQl_Oj-JyttIe0GcvLh5TtUJ5JKnTDMRh-RvQjf7yKMnitIj9-pnG2hQrh459XP68bTkA5bjZKxtq3mkjbPbDfn02eCKuDT0WDjQyjH_sJJ0qM4oLXRbObbu_Hn7zepOd5M4pbt-qJtcy-eb8_qnzQnjofMAxbR6Vyp_L5bQnBT5htK_ehtcJLnCWhbOJ3J6rjPPkQN3TQbkO5bRiLR_XWR_VDn3oyT3VXp0n3fRly5jtMgOBBJ0yQ4b4OR5JjxonDh83bG7MJPKtfD7H3KCbfCLWMUK; __yjs_duid=1_6c7a0f63c0a0d4012cbde204a2f9e41b1631265899762; REALTIME_TRANS_SWITCH=1; FANYI_WORD_SWITCH=1; SOUND_SPD_SWITCH=1; HISTORY_SWITCH=1; SOUND_PREFER_SWITCH=1; BDORZ=B490B5EBF6F3CD402E515D22BCDA1598; H_PS_PSSID=; delPer=0; PSINO=1; BAIDUID_BFESS=CB0D780F4BB4AB7E7DF34F2BDD210638:FG=1; BA_HECTOR=2k848k0l218k002g2m1gmibjd0r; Hm_lvt_64ecd82404c51e03dc91cb9e8c025574=1631844371,1634283119,1634283131; Hm_lpvt_64ecd82404c51e03dc91cb9e8c025574=1634284358; __yjs_st=2_Njc0MzhjYjU1ZTU4ODkyZjE4MTJhOGVmOWRhMWQyZGMzNzc5ZDBkYmYwNTU2YzE3MzdlYmVhN2Y5NmVmN2QyZDgxMmI1MjJjOTc1ZWYxNmUzNWJmMTJmYjNmNWY3NmQzMDE1NWQ0ZWNkMjAyNzU0ZGIxZmZlNmI2NjViZTgyOGViZmJhNmQ2NTdkN2M1YWUwNDhhMTA0YzZiZDdmOTg1MGNiZmFkMmRiMDU4YWJhMDU5ZGZkNTQzZWRhN2Q3MjJjY2FkMTNjMGQ5NWNmMzhmMjA1YzNmYjFiN2ZlZGFiMTg5NGI4ZTViZmViY2ZlNDYwMmFjMTQxNzJkODE4MWJiMl83X2M5MzYwYWZj; ab_sr=1.0.1_YjAyN2EyMTNhOWI5NmZmNmUxMWQ2ODc1ZDE4MDI5NzVmZDZhYmM3YmFhMWVhMmE4ZGU4N2FmNjVlNzExNTlhNjFiMWNiMGFkNWY4MWMxNTBmM2FkZDc1ZTU2NmVhYzQ0MDJmOWY1NDBhNDNiMjg1OTgwNGEzNzgyMWQ4NmE5NTQwOTIzYmE1YmM4MjVlOWRkMjlmYjZiNzQ2NmNjZmVkZA==',
    'Host':' fanyi.baidu.com',
    'Origin': 'https://fanyi.baidu.com',
    'Referer': 'https://fanyi.baidu.com/?',
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
    'domain': 'common',
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

![success](https://github.com/1255234553/skills/blob/main/crawl%20success.png)

