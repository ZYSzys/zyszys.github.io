---
layout: post
category: Front-end
title: CSS box-shadow属性
tags: 
    CSS
---

### 用法:  
```css
body {
    box-shadow: inset x-offset y-offset blur-radius spread-radius color;
              /*投影方式|水平偏移量|垂直偏移量|模糊半径|扩展半径｜阴影颜色   可多个阴影并列，逗号隔开*/
}
```

### 取值:  
* 投影方式: inset/无   可选，默认方式为外阴影，inset设置为内阴影。
* 水平偏移量: 若为正值，阴影在盒子右边；若为负值，阴影在盒子左边。
* 垂直偏移量: 若为正值，阴影在盒子下边；若为负值，阴影在盒子上边。
* 模糊半径: 可选且>=0，值为0时阴影不具有模糊效果，值越大阴影边缘越模糊。
* 扩展半径: 可选，正值阴影扩大，负值阴影缩小。
* 阴影颜色: 可选，不选时浏览器取默认颜色值。


### 写法:
```css
body {
    -moz-box-shadow: ......  /*Firefox*/
    -webkit-box-shadow: ......  /*Safari, Google Chrome*/
    box-shadow: ......  /*IE等其它浏览器*/
}
```
