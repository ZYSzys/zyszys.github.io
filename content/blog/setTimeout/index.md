---
title: 一道经典面试题-----setTimeout(function(){}，0)
date: "2018-05-10T20:40:32.169Z"
descripton: 转载：[一道经典面试题-----setTimeout(function(){}，0)]
---


转载：[一道经典面试题-----setTimeout(function(){}，0)](https://www.cnblogs.com/destinyruru/p/5823760.html)

先看题：
```js
for (var i = 0; i < 3; i++) {
    setTimeout(function() {
        console.log(i);
    }, 0);
    console.log(i);
}
```
结果是：`0 1 2 3 3 3`  
很多公司面试都爱出这道题，此题考察的知识点还是蛮多的。 都考察了那些知识点呢？  
**异步、作用域、闭包**。  
<!--more-->
我们来简化此题：
```js
setTimeout(function() {
    console.log(1);
}, 0);
console.log(2);   //先打印2，再打印1
```
因为是setTimeout是异步的。  
正确的理解setTimeout的方式(注册事件)： 有两个参数，第一个参数是函数，第二参数是时间值。  调用setTimeout时，把函数参数，放到事件队列中。等主程序运行完，再调用。

就像我们给按钮绑定事件一样：
```js
btn.onclick = function() {
    alert(1);
};
```
这么写完，会弹出1吗。不会！！只是绑定事件而已！  必须等我们去触发事件，比如去点击这个按钮，才会弹出1。

setTimeout也是这样的！只是绑定事件，等主程序运行完毕后，再去调用。  
setTimeout的时间值是怎么回事呢？
`setTimeout(fn, 2000)`  
程序会不会报错？ 不会！而且还会准确得打印1。为什么？ 因为真正去执行console.log(i)这句代码时，var i = 1已经执行完毕了！

所以我们进行dom操作。可以先绑定事件，然后再去写其他逻辑。
```js
window.onload = function() {
    fn();
}
var fn = function() {
    alert('hello')
};
```
这么写，完全是可以的。因为异步！

es5中是没有块级作用域的。
```js
for (var i = 0; i < 3; i++) {}
console.log(i); //3，也就说i可以在for循环体外访问到。所以是没有块级作用域。
```
这回我们再来看看原题。  
原题使用了for循环。循环的本质是干嘛的？ 是为了方便我们程序员，少写重复代码。

原题等价于：
```js
var i = 0;
setTimeout(function() {
    console.log(i);
}, 0);
console.log(i);
i++;
setTimeout(function() {
    console.log(i);
}, 0);
console.log(i);
i++;
setTimeout(function() {
    console.log(i);
}, 0);
console.log(i);
i++;
```
因为setTimeout是注册事件。根据前面的讨论，可以都放在后面。  
原题又等价于如下的写法：
```js
var i = 0;
console.log(i);
i++;
console.log(i);
i++;
console.log(i);
i++;
setTimeout(function() {
    console.log(i);
}, 0);
setTimeout(function() {
    console.log(i);
}, 0);
setTimeout(function() {
    console.log(i);
}, 0);  //弹出 0 1 2 3 3 3
```
怎么保证能弹出0，1， 2呢？
```js
for (var i = 0; i < 3; i++) {
    setTimeout((function(i) {
        return function() {
            console.log(i);
        };
    })(i), 0);  //改为立即执行的函数
    console.log(i);  
}
```

