---
title: 记一次百度前端面试
date: "2018-04-22"
description: 一次偶然间在baidu.com右击点了一下检查元素，意外的发现百度的招聘信息存在html元素顶部，于是点了进去，抱着试试看的态度投了求职前端工程师的简历。意料之外的过了笔试，并经历了人生的一次实习面试。
---

一次偶然间在baidu.com右击点了一下检查元素，意外的发现百度的招聘信息存在html元素顶部，于是点了进去，抱着试试看的态度投了求职前端工程师的简历。意料之外的过了笔试，并经历了人生的一次实习面试。

<!--more-->
由于是远程面试，我在规定时间之前打开Chrome进入了面试房间，没过多久就收到了面试官的面试邀请。先简单做了一下自我介绍，就开始了人生的一次实习面试。。。

## 说一下http状态码

[HTTP状态码](http://www.runoob.com/http/http-status-codes.html)

下面是常见的HTTP状态码：
- 200 - 请求成功
- 301 - 资源（网页等）被永久转移到其它URL
- 404 - 请求的资源（网页等）不存在
- 500 - 内部服务器错误

### HTTP状态码分类

- 1**   信息，服务器收到请求，需要请求者继续执行操作
- 2**	成功，操作被成功接收并处理
- 3**	重定向，需要进一步的操作以完成请求
- 4**	客户端错误，请求包含语法错误或无法完成请求
- 5**	服务器错误，服务器在处理请求的过程中发生了错误

### HTTP状态码列表

```
100(Continue): 继续。客户端应继续其请求  
101(Switching Protocols): 切换协议。服务器根据客户端的请求切换协议。只能切换到更高级的协议，例如，切换到HTTP的新版本协议  

200(OK): 请求成功。一般用于GET和POST请求
201(Created): 已创建。成功请求并创建了新的资源  
202(Accepted): 已接受。已经接受请求，但未处理完成  
203(Non-Authoritative Information): 非授权信息。请求成功。但返回的meta信息不在原始的服务器，而是一个副本  
204(No Content): 无内容。服务器成功处理，但未返回内容  
205(Reset Content):  重置内容。服务器处理成功，用户终端（例如：浏览器）应重置文档视图。可通过此返回码清除浏览器的表单域  
206(Partial Content): 部分内容。服务器成功处理了部分GET请求 

300(Multiple Choices): 多种选择。请求的资源可包括多个位置，相应可返回一个资源特征与地址的列表用于用户终端(浏览器)选择
301(Moved Permanently): 永久移动。请求的资源已被永久的移动到新URI，返回信息会包括新的URI，浏览器会自动定向到新URI。今后任何新的请求都应使用新的URI代替
302(Found): 临时移动。与301类似。但资源只是临时被移动。客户端应继续使用原有URI
303(See Other): 查看其他地址。与301类似。使用GET和POST请求查看
304(Not Modified): 未修改。所请求的资源未修改，服务器返回此状态码时，不会返回任何资源。客户端通常会缓存访问过的资源，通过提供一个头信息指出客户端希望只返回在指定日期之后修改的资源
305(Use Proxy): 使用代理。所请求的资源必须通过代理访问
306(Unused): 已经被废弃的HTTP状态码
307(Temporary Redirect): 临时重定向

400(Bad Request): 客户端请求的语法错误，服务器无法理解
401(Unauthorized): 请求要求用户的身份认证
402(Payment Required): 保留，将来使用
403(Forbidden): 服务器理解请求客户端的请求，但是拒绝执行此请求
404(Not Found): 服务器无法根据客户端的请求找到资源。
405(Method Not Allowed): 客户端请求中的方法被禁止

......
```

## GET和POST的区别  

1.get是从服务器上获取数据的请求，post是向服务器传送数据的请求   
2.get传送的数据量较小，post可以传递的数据比get多  
3.get安全性低，post安全性较高，但执行效率比post好  

## 事件绑定、事件监听、事件委托

[事件委托](https://github.com/yangshun/front-end-interview-handbook/blob/master/Translations/Chinese/questions/javascript-questions.md#请解释事件委托event-delegation)

## webpack基本用法

[webpack官方文档](https://webpack.js.org/concepts/)

## this

[javascript中的this](https://github.com/yangshun/front-end-interview-handbook/blob/master/Translations/Chinese/questions/javascript-questions.md#请简述javascript中的this)

## 原型和原型链

[原型继承的工作原理](https://github.com/yangshun/front-end-interview-handbook/blob/master/Translations/Chinese/questions/javascript-questions.md#请解释原型继承prototypal-inheritance的工作原理)

## 实现函数add使得`add(1)(2)(3)=1+2+3=6`

很基础的一个柯里化函数  
```js
function add(a) {
  return function(b) {
    return function(c) {
      return a+b+c
    }
  }
}

add(1)(2)(3) // => 6
```

或者使用ES6的箭头函数(**推荐**)

```js
const add = a => b => c => a+b+c

add(1)(2)(3) // => 6
```
