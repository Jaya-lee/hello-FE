# AntDesign

官网： https://ant.design/index-cn

> ANT DESIGN 是蚂蚁金服体验技术部出品的一个设计&前端框架,基于 React 框架

先说点题外话：今天又看到了知乎上关于该选择前端的那三大框架这种话题，大家据理力争，各有道理。我也是默默的翻了翻评论然后一笑而过，怎样，我就是选react你咬我啊。讲道理我也是`尤小右`的小迷妹，vue我刚上手时一脸懵：这就可以了？这么简单？这逻辑分析都不需要我了？确实，我也觉得简单就是王道啊，有捷径干嘛不走，又不是你用了一堆props来修改state(react框架)就感觉自己牛逼到不行，赶快洗洗睡吧。

我用react的感想是：这才是一个生态体系。抛开全家桶以及衍生出来的一堆旁支，就UI库来说就有material-ui,AntDesign这两大库来支持react，真心赞。

回归话题：那么本节jaya给大家总结了一下它的使用方法，因为没有`bootstrap`那么简单的直接一个class就可以解决，不过不用担心，跟jaya一步步来开始你的AntDesign

说明：因为antd是针对react的库，所以这里我详细的介绍在`create-react-app`创建的项目中如何使用antd组件，并对`webpack`做一定的配置满足`按需加载`


1.安装create-react-app
```
$ npm install -g create-react-app

```
create-react-app 是业界最优秀的 React 应用开发工具之一

2.新建项目，进入

```
$ create-react-app antd-demo
$ cd antd-demo
```
３．安装并引入antd

```
$ npm i antd --save
```
4.按需加载css,js
