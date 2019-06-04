## 整体功能描述

<p align="center">
  <img src="https://i.loli.net/2019/05/22/5ce4f2d09e77326615.png">
</p>

> A vue page stack manager Vue页面堆栈管理器

[预览](https://hezhongfeng.github.io/vue-page-stack-example/)

[示例源码](https://github.com/hezhongfeng/vue-page-stack-example)

Vue页面堆栈管理器，一个在移动端`Web App`使用的，模仿原生App的`UI Stack`的一个插件。主要功能是能够实现页面前进的时候刷新，后退的时候返回原页面。例如：
`A->B`，新渲染页面B,`back`一下就会返回到A，并且A的状态是进入B时候的状态，不需要重新渲染，同时有activited的钩子激活。

## 功能说明

1. 在vue-router上扩展，原有导航逻辑不需改变
2. `push`或者`forward`的时候重新渲染页面，Stack中会添加新渲染的页面
3. `back`或者`go(负数)`的时候不会重新渲染，从Stack中读取先前的页面，会保留好先前的内容状态，例如表单内容，滚动条滑动的位置等
4. `back`或者`go(负数)`的时候会把不用的页面从Stack中移除
5. `replace`会更新Stack中页面信息
6. 回退到之前页面的时候有activited钩子函数触发
7. 支持浏览器的后退，前进事件
8. 支持响应路由参数的变化，例如从 /user/foo 导航到 /user/bar，组件实例会被复用
9. 可以在前进和后退的时候添加不同的动画，也可以在特殊页面添加特殊的动画

## 安装和用法

```
npm install vue-page-stack
# OR
yarn add vue-page-stack
```

### 注册

```
import Vue from 'vue'
import VuePageStack from 'vue-page-stack';

// vue-router是必须的
Vue.use(VuePageStack, { router }); 
```

```
// App.vue
<template>
  <div id="app">
    <vue-page-stack>
      <router-view ></router-view>
    </vue-page-stack>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
    };
  },
  components: {},
  created() {},
  methods: {}
};
</script>

```

## API

### 注册
注册的时候可以指定VuePageStack的名字和keyName
```
Vue.use(VuePageStack, { router, name: 'VuePageStack', keyName: 'stack-key' });
```

### 前进和后退
可以在`router-view`的页面watch `$route`，通过`stack-key-dir(自定义keyName这里也随之变化)`参数判断此时的方向，可以参考[实例](https://hezhongfeng.github.io/vue-page-stack-example/)

## 相关说明

### keyName
为什么会给路由添加`keyName`这个参数，是为了支持浏览器的后退，前进事件，这个特点在微信公众号和小程序很重要

## 感谢
这个插件同时借鉴了[vue-navigation](https://github.com/zack24q/vue-navigation)和[vue-nav](https://github.com/nearspears/vue-nav)，很感谢他们给的灵感。
