---
title: Vue封装canvas-nest组件
date: "2018-06-24T20:40:32.169Z"
description: 为了能在Vue上更简便地使用 canvas-nest.js 这个炫酷的特效，花了几小时直接将canvas-nest封装成了 vue-canvas-nest 组件。
---

![vue-canvas-nest效果](./vue-canvas-nest.png)

为了能在Vue上更简便地使用[canvas-nest.js](https://github.com/hustcc/canvas-nest.js)这个炫酷的特效，在原项目作者的提醒下，花了几小时直接将canvas-nest封装成了[vue-canvas-nest](https://github.com/ZYSzys/vue-canvas-nest)组件。

<!--more-->

## 初始化
```bash
# init
vue init webpack-simple vue-canvas-nest
# install dependencies
cd vue-canvas-nest && npm install
```

## 安装原项目依赖
```bash
npm install canvas-nest.js
```

## 编写组件
仔细阅读一下原项目的README，发现它只有一个API，并且作者已经说明了如何使用，只需传入需要渲染的元素和canvas-nest配置:
```js
// There is only one API, use it like:

import CanvasNest from 'canvas-nest.js';

const config = {
  color: '255,0,0',
  count: 88,
};

// render nest on element with config.
const cn = new CanvasNest(element, config);

// destroy
cn.destroy();
```

将原来的```src```文件夹重命名为```example```以便后期当示例和调试使用。

新建```src```文件夹，并在```src```文件夹下建立文件```vueCanvasNest.vue```，代码如下：

```html
<template>
  <div class="vue-canvas-nest-element" style="position: absolute;top: 0;left: 0;right: 0;bottom: 0;z-index: -1;">
  </div>
</template>
<script>
import CanvasNest from 'canvas-nest.js';
export default {
  name: 'vueCanvasNest',
  props: {
    config: {
      type: Object,
      default () {
        return {
          color: '255,0,0',
          count: 88,
        }
      }
    }
  },
  data() {
    return {
      cn: ''
    }
  },
  mounted() {
    const el = document.querySelector('.vue-canvas-nest-element')
    this.cn = new CanvasNest(el, this.config)
  },
  beforeDestroy() {
    this.cn.destroy()
  }
}
</script>
```

同时新建一个叫```index.js```导出组件
```js
import vueCanvasNest from './vueCanvasNest.vue'

export default vueCanvasNest
```

## 示例测试
在```example```文件夹下的```App.vue```文件里加入组件  
javascript标签中代码：
```js
import vueCanvasNest from '../'
export default {
  name: 'app',
  components: { vueCanvasNest },
  data() {
    return {
      msg: 'Welcome to Your Vue.js App',
      config: {
        color: '0,0,255',
        count: 200,
      }
    }
  }
}
```
template标签中加入一行：
```html
    <vue-canvas-nest></vue-canvas-nest>
```

## 更改webpack.config.js

entry改为 ./src/index.js 
```javascript
module.exports = {
    entry: './src/index.js',
    ...
}
```

开发环境下entry改为 ./example/main.js
```javascript
if (process.env.NODE_ENV === 'production') {
  ...
} else {
  module.exports.entry = './example/main.js'
}
```

## 运行
```bash
npm run dev
```
此时就能看到炫酷的canvas-nest效果了

## 发布组件到npmjs
```bash
# npm初始化
npm init 

# 按照提示完成package.json后
npm publish
```

## 项目完整地址：[vue-canvas-nest](https://github.com/ZYSzys/vue-canvas-nest)