
网站运行需要有大量的数据的读取，同时用户也需要把自己的数据存储到服务器，对于海量数据的操作。 就需要有专门的软件配合，这个软件就是数据库。

当前比较流行的数据库，Oracle 甲骨文，SQL server ，这些都是商业数据库。但是，开源数据库目前更受青睐。一个是 Mysql , 另一个是 MongoDB 。

## MongoDB

 MongoDB 的官网: https://www.mongodb.com/

 MongoDB 中文社区: http://www.mongoing.com/

 MongoDB 中文网:  http://www.mongodb.org.cn/

- MongoDB：是一个数据库软件，有时候我们简称它叫一个数据库，但是其实一个 MongoDB 运行起来，可以里面同时运行多个数据库
- Database: 数据库。一般做法是，一个项目对应一个数据库。
- Collection: 集合。类似于关系型数据库下的*表*的概念，例如全班同学信息。
- Document：文档。一个集合中会包含多个文档（一个文档中存储一个同学的信息）。文档对应关系型数据库中的 *记录* 这个概念。

举例子来说，一个项目叫 facebook ，那么我们就建立一个 database 来存储这个项目的所有数据。
一个数据库中，可以创建多个集合，比如 users 。一个 users 集合中，可以包含多个文档，每个文档中存储一个 user 的信息（信息可以有多项：email, name, brithday ...）。

##　安装MongoDB

linux按照[这里](http://docs.mongoing.com/manual-zh/tutorial/install-mongodb-on-ubuntu.html)
可以安装新的版本

```
1.$ sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6

2.$ echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list

3.$ sudo apt-get update

4.$ sudo apt-get install -y mongodb-org
```

苹果系统上，用 HomeBrew 安装

```
brew install mongodb
```
安装好后，现在开始使用

## 通过命令行操作 MongoDB

1.首先创建一个文件来存储数据
```
mkdir data/db
```
2.启动mongodb

```
mongod --dbpath=./data/db

```
命令就是 `mongod `,后面传递的选项就是给出存储的位置。

tip:使用过程中一定要保证mongodb的启动

3.进行数据库操作，开启Mongo Shell

```
mongo
```

### 插入一条数据

参考：
- [好奇猫课程](http://haoqicat.com/react-express-api/2-mongodb)

一条数据，应该保存成一个什么单位？数据库？集合？文档？

答案：一个文档。那么要保存一个文档，先要有一个数据库，再创建一个集合，然后集合中
才能插入这个文档。这个是**总体思路**。

具体操作步骤如下：

第一步，创建一个数据库

```
$ use express
switched to db express
```

下面的输出 `switched to db express` 意思是：已经切换到 express 这个数据库里面了。

查看数据库有没有创建成功，可以用

```
show dbs
```

暂时，没有保存数据到该数据库，所以，输出中没有 express 。


第二步，创建集合

创建集合，集合名称叫 users

```
> db.createCollection('users')
{ "ok" : 1 }
```

第三步，把一条数据，保存成一条文档（ Document ）

```
> db.users.insert({username: 'peter', email: 'peter@peter.com' })
WriteResult({ "nInserted" : 1 })
```

输出结果 `WriteResult({ "nInserted" : 1 })` 表示成功写入一条数据。

第四步，列出一个集合中的所有文档：

```
db.users.find()
```

### 对数据记录进行增删改查

第一步，增。

使用 insert() 接口。

```
> db.users.insert({username: 'billie', email: 'billie@billie.com'})
```

第二步，改。

使用 update() 接口。

```
 db.users.update({_id: ObjectId("584b62b830a2a2cbf4c4c3f6")}, {username: "billie66", email:"billie@billie.com"})
```

update 接口中有两个参考，第一个是查询条件，用来定位要更新的是哪一个文档，后面是更新后的数据。

第三步，查。

使用 find() 接口。

```
db.users.find({})
```

可以列出所有的 users 集合中的文档。

第四步，删。

使用 remove() 接口。


删除特定一个文档：

```
> db.users.remove({_id:  ObjectId("584b5dbf30a2a2cbf4c4c3f5")})
WriteResult({ "nRemoved" : 1 })
```

删除集合中所有文档：

```
> db.users.remove({})
```

基本命令就列举这些。我们发现敲命令比较麻烦，所以，可以考虑使用图形化的界面来操作 MongoDB 。

## 图形化的操作界面 mongo-express

Mongo-express 是一个用 express 技术开发的，MongoDB 的 GUI (图形界面)。可以方便美观的 操作 MongoDB 中的数据。

参考：http://haoqicat.com/hand-in-hand-react/4-mongo-express

全局安装：

```
npm install -g mongo-express
```

mongo-express 装好之后，我们需要通知它到底要连接到哪个数据库，通过修改 mongo-express 的配置文件来搞定。

所以首先第一步，我们先要找到　mongo-express 的配置文件。下面的这个命令可以帮我们找到 mongo-express 的安装位置：

```
$ npm list -g mongo-express
/home/peter/.nvm/versions/node/v7.1.0/lib
```

找到后，就可以进入安装文件夹来修改配置文件了。

```
cd /home/peter/.nvm/versions/node/v7.1.0/lib
cd node_modules
cd mongo-express
cp config.default.js config.js
```

最后一步，就是把样例配置文件  config.defualt.js ，改名为真实的配置文件　config.js , 也就是说是程序会自动读到的配置文件。

打开配置文件，把

```
mongo = {
  db:       'db',
  username: 'admin',
  password: 'pass',
  ...
  url:      'mongodb://localhost:27017/db',
};
```

改为

```
mongo = {
  db:       'express',
  username: '',
  password: '',
  ...
  url:      'mongodb://localhost:27017/express',
};
```

上面的　`express` 就是我们要操作的数据库的名字，这个是通过　mongo shell 中，执行`show dbs`看到的。由于我们的 `express` 这个数据库本身没有设置密码，所以上面 `username` 和 `password` 两项都改成空字符串就可以了。

同时，mongo-express 这个软件自己还有自己登陆的用户名和密码，并且有默认值，通过　config.js 中这几行：

```
basicAuth: {
  username: process.env.ME_CONFIG_BASICAUTH_USERNAME || 'admin',
  password: process.env.ME_CONFIG_BASICAUTH_PASSWORD || 'pass',
}
```

用户名是　`admin` ，密码是　`pass` 。

启动　mongo-express 需要开启一个新的命令行标签。然后输入

```
$ mongo-express
```

输出如下

```
Mongo Express server listening at http://localhost:8081
basicAuth credentials are "admin:pass", it is recommended you change this in your config.js!
Connecting to express...
```

浏览器中打开 http://localhost:8081 可以开始使用 mongo-express 了。


# 总结

这节中我们分别用 Mongo Shell 和 mongo-express 两种方式，对 mongodb 数据库进行了操作。但是，最重要的是下节介绍的如何在 JS 代码中来操作 mongodb 。
