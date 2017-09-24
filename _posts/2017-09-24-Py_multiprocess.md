---
layout: post
category: Python
tags: 
    Python
    多进程
title: Python -- multiprocessing
---
python中的多线程其实并不是真正的多线程，并不能做到充分利用多核CPU资源，都说python多线程是个鸡肋。想要充分利用，在python中大部分情况需要使用多进程，那么这个包就叫做 multiprocessing。
<!--more-->
# multiprocessing

## Process
```python
#!/usr/bin/env python
#-*- coding: utf-8 -*-

__author__ = 'ZYSzys'

from multiprocessing import Process, Lock
import time

class MyProcess(Process):#创建自己的进程类
    """docstring for MyProcess"""
    def __init__(self, loop, lock):
        Process.__init__(self)
        self.loop = loop
        self.lock = lock

    def run(self):
        for count in range(self.loop):
            time.sleep(0.1)
            self.lock.acquire()#开启进程锁🔒，以免产生’互斥‘
            print 'Pid: ', self.pid, ' LoopCount: ', count ,'\t%s' % time.ctime()
            self.lock.release()#释放进程锁🔒
        

def process(num):
    time.sleep(1)
    print 'process: ', num, '\t%s' % time.ctime()

if __name__ == '__main__':
    lock = Lock()
    for i in range(2, 10):
        p = MyProcess(i, lock)
        #p.daemon = True #如果设置为True，当父进程结束后，子进程会自动被终止。
        p.start()
        #p.join() #所有子进程都执行完了然后再结束

    for i in range(5):
        p = multiprocessing.Process(target=process, args=(i, ))
        p.start()
    print 'CPU: ', multiprocessing.cpu_count()#CPU核数
    for p in multiprocessing.active_children():
        print 'Child name: '+p.name  +'id: ' + str(p.pid)#子进程

    print 'Process end'
```

## Pool
```python
#!/usr/bin/env python
#-*- coding: utf-8 -*-

__author__ = 'ZYSzys'

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
    p = Pool(processes=4)#设置四个进程
    urls = [
    'https://www.baidu.com',
    'http://www.meituan.com/',
    'http://blog.csdn.net/',
    'http://xxxyxxx.net'
    ]
    p.map(crawl, urls)#将url映射进crawl函数

```
![multiprocessing.Pool](/assets/images/Py1.png)
## 参考
[Python爬虫进阶六之多进程的用法](http://cuiqingcai.com/3335.html)
