# vue-router

官网文档：http://router.vuejs.org/zh-cn/

```
npm install vue-router
```
它的写法类似reat-router第三版

## 语法

新建一个router.js文件

```
import Vue from 'vue'
import VueRouter from 'vue-router'
 Vue.use(VueRouter)
// 1. 定义（路由）组件。
// 可以从其他文件 import 进来
const Home={  template: '<div>home</div>'}
const Foo = { template: '<div>foo</div>' }
const Bar = { template: '<div>bar</div>' }

// 2. 定义路由
// 3. 创建 router 实例，然后传 `routes` 配置
const router = new VueRouter({
  routes :[
    { path: '/', component: Home },
    { path: '/foo', component: Foo },
    { path: '/bar', component: Bar }
  ]
})

// 4. 创建和挂载根实例。
// 记得要通过 router 配置参数注入路由，
// 从而让整个应用都有路由功能
export default router

```
然后在入口main.js里挂载上
```
import router from './router'

/* eslint-disable no-new */
new Vue({
  ...

  router,
  ...
```
在App.vue中

```
<router-link to='/'>Home</router-link>
<router-link to='/foo'>Foo</router-link>
<router-link to='/bar'>Bar</router-link>
<router-view></router-view>
```
router-view作用是在路径中匹配到对应的组件
router-link实现跳转

## 动态路由

```
const User = {
  template: '<div>User</div>'
}

const router = new VueRouter({
  routes: [
    // 动态路径参数 以冒号开头
    { path: '/user/:id', component: User }
  ]
})
```
获取id值，或者是别的由router注入的方法时，我们可以通过`this.$route.params`拿到

在模板中直接`$route.params.id`来拿

```
const User = {
  template: '<div>User {{ $route.params.id }}</div>'
}
```

## 路由嵌套

我要在/foo下再嵌套一个/aaa

```
children属性

{ path: '/foo', component: Foo ,
    children:[
      {path:'aaa',component:Aaa}
    ]},

这样路由规则就多了一条/foo/aaa
为了使Aaa组件显示,还需在Aaa的父组件Foo加router-view  

```
再嵌套时就再写一级children就可以了

## 命名路由

链接到一个命名路由，可以给 router-link 的 to 属性传一个对象：

```
<router-link :to="{ name: 'user', params: { userId: 123 }}">User</router-link>
```
## 重定向与别名

重定向:
```
routes: [
   { path: '/a', redirect: '/b',component: A, }
 ]
```
别名:

```
routes: [
    { path: '/a', component: A, alias: '/b' }
  ]
```
两者的区别是:

重定向中挂载A,url会由/a变为/b
而别名url不会发生改变,也就是一个组件有两个路由.
