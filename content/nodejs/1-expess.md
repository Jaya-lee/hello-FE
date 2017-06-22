# Hello Express

React 是一个 **前端框架** ，前端框架是运行在浏览器环境下的，负责 UI（ User Interface 用户界面）。

想一想，如果只有 UI ，那么用户要看的数据从哪里来？用户需要保存的数据如何进行运算之后保存到数据库中？这部分的功能就需要后端代码来完成。

当下实现后台服务，最流行的方式之一就是使用 Nodejs , Express 就是 Nodejs 的一个框架，而且是 Nodejs 各种后台框架中最为通用，最为流行的一个，没有之一。所以学习 Nodejs
最佳途径就是从 Express 入手。

## [Express](http://www.expressjs.com.cn/)是干什么的

> Express  
  基于 Node.js 平台，快速、开放、极简的 web 开发框架。

官网上，首页最能吸引我们注意的就是 **API** 这个关键字。API （ Application Program Interface ）是**应用开发接口**，简称**接口** 。而Express 就是用来制作后台接口的，或者说叫制作后台 API 的。

tips:UI/API 都是接口，同时都是给人用的，但是他们有什么区别呢。

```
UI:程序跟用户（ User ）的接口
API:程序跟程序或者说程序员的接口,API 分多种，我们下面专门瞄准的是 Web API 或者叫 HTTP API
```

## 用express实现hello World

对express有了基本的认识后，现在写一个小程序

1.新建文件夹，初始化为一个 nodejs项目

```
mkdir express
cd express
npm init -y
```

文件夹内就会生成一个 package.json ，有了这个文件，我们这个文件夹就可以
叫做一个 **Nodejs 项目** 了 。

2.装包

```
npm i --save express
```

tips：一个常见装包错误，如果我们项目文件夹的名和要装的包名同名是会报错的，解决方法就是rename文件夹的名字

### 语法用 ES6 ？

我们的前台代码，因为有 Babel 的支持，可以全部采用 ES6来写。后台代码，我们会让它直接运行在 Nodejs上(eg. java运行在jvm上)

我们在 [Node.green 网站](http://node.green/)上，可以看到新版的 Nodejs (7.0 版本以上)对于 ES6 的支持已经到了99% 。所以，不用 Babel 我们也可以直接使用 ES6 语法，但是唯一要注意的就是不能用 import （ 也就是说 nodejs 是不支持 ES6 模块语法的），我们的后台代码暂时需要用 require 来替代 import 。require 用的是 commonjs 模块语法，这个是 Nodejs 原生支持的。

>总结: 可以用ES6，别用 import 就好了。

OK,GO ON!

3.开始运行

参考[官网教程](http://www.expressjs.com.cn/starter/hello-world.html)，我们来写 Hello World 。

到项目中，创建一个 index.js 文件，内容如下：

```js
const express =  require('express');
const app = express();

app.listen(3000, () => console.log('running on port 3000...'))
```

上面三句代码，我们就自己动手实现了一个**服务器**( server ) 。服务器（这里指的是软件）的作用是，始终监听客户端的请求，或者说前端不给服务器发信号，服务器
就什么都不做，但是也不死，只是去循环执行，或者就叫**始终在监听**（listen）。

上面的 `3000` 指的是 **3000端口** port ，一个服务器好比一座大厦，有很多个门，3000 是其中一个门的门牌号。

这里使用了回调函数，方便我们看出输出。一般回调函数的使用场合就是，之前的一个操作耗时比较长（或者是一直监听事件，例如 onClick()）这样的情况下才使用回调函数。

4.上面的程序执行，就到后台运行

```
node index.js
```
因为我们写的 index.js 是一个 nodejs 程序，所以用 node 命令去执行，这个执行过程跟浏览器已经脱离了。这个 也基本上是我们到目前为止，唯一一个可以脱离浏览器执行的 JS 程序。

运行结果:

```
$ node index.js
running on port 3000...
```

OK,现在我们的服务器已经运行起来了，它就一直监听端口，根据端口的请求来执行操作。这个请求是由客户端完成的。

### 客户端请求

现在我们需要的客户端请求是，一个

```
GET /
```

同时这个请求，必须来自3000端口。

可以发请求的方式不唯一，可以用浏览器地址栏，可以用页面的 form 发，也可以用 axios 发，后者使用专门的 API 调试工具 curl/postman来发。

现在，我们就用浏览器的地址栏来发请求。地址栏中输入

```
http://localhost:3000/
```

我们在上面的 index.js 中，app.listen 语句的上面，添加如下代码：

```
app.get('/', () => {
  console.log('request come in...');
})
```
- get 是一个 http 请求的动词 ，类似的还有 post/delete/put (第四节)
- / 是一个路径 ，英文 path

一个动词加一个路径，这样就组成一个 HTTP 请求 ，公式如下

```
request = verb + path + data
```
这里的请求，是服务器端接收请求

请求之后，会发现浏览器里没有任何输出，这是因为，我们的 express 服务器根本就没有给前台返回任何字符串，回调函数中的 `console.log()` 只能把字符串打印到后台。

### 继续前面的代码：返回字符串

前面的回调函数中，console.log 打印字符串，只是出现在后端（服务器端）。前端得不到任何反馈。所以，我们可以把代码做如下修改

```js
app.get('/', function(req, res){
  res.send('Hello World');
})
```
`req` 是 request**请求**的简写，` res`是 response**响应**的简写。
`res.send('Hello World')`的作用是从后端向前端浏览器返回字符串 `Hello World` 。

### nodemon高效开发

每次修改代码我们都要重启一次`node index.js`，很麻烦，于是我们有高效的工具:`nodemon`。它可以助力 node 应用的开发效率，因为它能监测 node 应用目录中的各个文件，若文件有改动，nodemon 会自动重启你的 node 应用，再也不用手动重启了。

命令:

```
npm i nodemon -g
nodemon idnex.js
```
---

### 常见错误

```
Error：listen EADDRINUSE :::4000
```
EADDRINUSE:'地址已经被占用'

原因:本地已经有一个服务运行在4000端口了,地址冲突，可以修改端口或者停掉之前的服务

# 总结

到这里，我们一个 Express 的 Hello World API 就制作完毕。由这个点的学习，我们也发现了前端与后端的区别:

前端，front-end，或者也可以叫前台。后端，back-end 也可叫后台。

前端代码运行环境是什么呢？对于我们 Web 开发者来说，就是浏览器。注意，浏览器是安装在用户自己的机器上的。也就是说前端代码运行在我们自己的笔记本或者 ipad 上，如果前端代码写的烂，那么考验的是我们自己设备的内存大小。

后端代码运行环境是？是一个放在人家机房里的刀片机。上面一般都运行 Linux 操作系统。刀片机根本就没有显示器，当然也不能跑浏览器。所以后端代码的运行是脱离浏览器的。如果后端写的烂，那么考验的就是刀片机的内存够不够了。

然后，再从 API 的角度来聊聊。前端是 API 的消费者，后端是 API 的生产者。后台 API 写好之后，默认不运行，只有当前端发送过请求来的时候才会触发后台 API 代码运行。

当然，在平常开发的时候，我们并没购买刀片机，所有只能是用自己的笔记本来当刀片机用了。这时候，基本可以认为 express 写的代码就是后端代码，react 写的代码就是前端代码。

### 附:hello World全部代码

package.json 如下：

```
{
  "name": "express-hello",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "express": "^4.14.0"
  }
}
```
index.js 代码如下

```
const express =  require('express');
const app = express();


// 下面三行就是我们实现的一个 API
app.get('/', (req, res) => {
  res.send('Hello World')
})

app.listen(3000, () => {
  console.log('running on port 3000...')
})
```
上面两个文件都放在一个 express-hello 文件夹中，然后

```
cd express-hello
npm install
node index.js
```
代码就运行起来了
