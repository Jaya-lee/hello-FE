---
title: GitBook
---

# 什么是gitbook

>Modern documentation format and toolchain using Git and Markdown

使用git和markdown语法的现代文档格式

在这之前我也会写自己的电子笔记，博客这类的。但是想要查看的时候找起来太浪费时间。这时候就不得不赞一下**gitbook**这个神奇的工具

- markdown语法简直不要太好用
- 目录清晰，一看就知道有哪些点
- 自带search功能，虽然目前不太支持模糊匹配，但是比一页一页翻笔记爽太多了
- 本地or托管，想怎么看怎么看
- 使用git瞬间提升自己的逼格


# 使用gitbook

### [gitbook官网](https://www.gitbook.com)

### [github上对gitbook的使用方法进行了详细的介绍](https://github.com/GitbookIO/gitbook)


1.安装

```
npm i gitbook-cli -g
```

2.创建一个文件夹,进入,并初始化

```
gitbook init
```

3.这样会生成两个文件

- README.md 内容显示在最前，相当于封面

- SUMMARY.md 为目录

注:当每次修改了SUMMARY.md时,可通过 gitbook init 自动按目录创建文件

4.启动服务器查看和编辑命令
```
gitbook serve
```
然后在localhost:4000端口就可以看到这本书了

下面我们就开始使用了

----

修改目录:(截取我的一部分目录，大家可以按格式修改)

```
* Redux
    * thunk
        * [thunk的初步介绍](./Redux/thunk/1-thunk.md)
        * [为什么使用thunk](./Redux/thunk/2-thunk.md)
* 部署项目
    * [部署React](./部署项目/deploy.md)
* 数据库
    * [mongoDB](./数据库/1-mongodb.md)

```

OK,最最重要的来了

# 托管gitbook

1.在github上创建一个仓库

为了部署方便，将文件做一个调整，将所有文件放在文件夹content里面

2.生成一个node项目

```
npm init
```
生成一个package.json文件

3.将package.json文件中scripts改为如下代码

```js
"scripts": {
   "start": "gitbook serve ./content ./gh-pages",
   "build": "gitbook build ./content ./gh-pages",
   "deploy": "node ./scripts/deploy-gh-pages.js",
   "publish": "npm run build && npm run deploy",
   "port": "lsof -i :35729"
 }
```

4.创建.gitignore

```
忽略gh-pages
```

5.部署到master

```
git init
git add -A
git commit -m 'hello-fe'
git remote add origin git@github.com:Jaya-lee/hello-fe.git
git push -u origin master
```

6.部署到gh-pages

手动:

- 运行npm run build, 把md文件翻译为html文件，放在gh-pages文件夹
- 拷贝gh-pages中的文件，到本仓库的gh-pages分支，上传
- 以后每次修改完都要拷贝到gh-pages分支，很麻烦

自动:

- 使用一个npm包gh-pages

```
npm i gh-pages --save
```
- 加一段自动化脚本

创建scripts/deploy-gh-pages.js

```js
'use strict';

var ghpages = require('gh-pages');

main();

function main() {
    ghpages.publish('./gh-pages', console.error.bind(console));
}

```
- 在配置文件添加

```
"deploy": "node ./scripts/deploy-gh-pages.js",
```

- 运行

```
npm run publish
```
- 这样每次修改后再次执行 npm run publish 就可以了

[现在就可以看看你自己的gitbook了](https://Jaya-lee.github.io/hello-fe)
