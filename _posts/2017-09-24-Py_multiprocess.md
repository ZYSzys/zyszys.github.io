---
layout: post
category: Python
tags: 
    Python
    多进程
title: Python -- multiprocessing
---

```python
import time
from multiprocessing import Pool
import requests
from requests.exceptions import ConnectionError

def crawl(url):
    try:
        print requests.get(url)
    except ConnectionError:
        print 'Error', url
    finally:
        print 'URL: ', url, 'done', '\t%s' % time.ctime()

if __name__ == '__main__':
    p = Pool(processes=4)
    urls = [
    'https://www.baidu.com',
    'http://www.meituan.com/',
    'http://blog.csdn.net/',
    'http://xxxyxxx.net'
    ]
    p.map(crawl, urls)

```
