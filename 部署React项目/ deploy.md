# 部署React

写完了React项目后，如何让它上线让大家可以看到效果呢？

这里我们所讨论的是部署到github上

首先我们知道在github上部署一个简单的(用html,css,js)小项目时，会先创建一个gh-pages分支，然后在分支上有一个文件为index.html,这样我们便可以在https://jaya-lee.github.io/×××上面看到

我们知道react中所有的入口文件均为js文件，所以我们就需要借助打包工具(比如webpack)来打包项目，让它生成静态页面，放到gh-pages上


具体的有关webpack使用，配置就不在本节中说明了。大家先按照步骤来部署你的项目吧！

## 开始部署

第一步，进入项目

第二步，运行

```
npm run build

```
可以看到命令行会输出
```
The project was built assuming it is hosted at the server root.
To override this, specify the homepage in your package.json.
For example, add this to build it for GitHub Pages:

  "homepage" : "http://myname.github.io/myapp",

```
这个指的是:  
```
如果我们把项目托管到服务器根文件位置 myname.github.io 没有问题
但是，现在要托管到 .github.io/××× 就肯定不行
```

第三步，修改package.json文件

添加这行:
```
 "homepage" : "http://jaya-lee.github.io/TODO-redux",
```

第四步
```
npm install --save-dev gh-pages

```

## 部署完成

现在打开https://jaya-lee.github.io/TODO-redux

可能有些人有这样一个问题:where is my picture???


造成这种情况的原因也是一个打包工具的bug,因为它打包的时候会造成路径的更改，然后找不到正确图片了。而且这种bug有可能今天有，明天就没有了，没必要深究它


#### 解决方法


1.图片全部为绝对路径

也就是引入公网的链接。这样可以保证路径不会因环境变化找不到

2.将图片都放到src文件夹下

这样又简单又好用，然后将路径修改一下，然后执行

```
npm run deploy
```
