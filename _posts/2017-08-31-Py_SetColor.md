---
layout: post
title: Python -- 通过PIL为图片填充背景色
category: Python
tags:
  - Python
  - tool
---

图片有些是没有背景颜色，如果希望以单色（比如白色）填充背景，可以使用下面的代码，这段代码将当前目录下的 1.jpeg 图片填充了白色背景。
使用指定的颜色的背景色即可，然后把该图片用alpha通道填充到该单色背景上。


<!--more-->

比如下面使用白色背景：

```python
#!/usr/bin/env python
#-*- coding: utf-8 -*-

__author__ = 'ZYSzys'

from PIL import Image

im = Image.open('1.jpeg')
# print im.getcolors() #获取图片颜色
x, y = im.size
try:
	# 设置图片背景色为白色
	temp = Image.new('RGBA', im.size, (255, 255, 255))
	temp.paste(im, (0, 0, x, y), im)
	temp.save('1.jpeg')
	print 'Set background white succeed.'
except:
	print 'Set background white failed.'
```