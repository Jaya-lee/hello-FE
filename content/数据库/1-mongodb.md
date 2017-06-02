# hello mongoDB

安装
[mongodb](http://docs.mongoing.com/manual-zh/tutorial/install-mongodb-on-ubuntu.html)


1.
2.
3.
4.


查看库 show dbs
使用某库 use test
现在所处的库 db
切换到这个库，删除 db.dropDatabase()

查看当前数据库下的所有集合  show tables/show collections
users为集合名称
插入数据  db.users.insert({name:'jaya',age:21})
查看数据    db.users.find() 有一个id find里面可以加对象
删除数据    db.users.remove({query})
若想全部删除 ，则db.remove({}) {}表示空的条件


更新数据    db.users.update({name:"jaya"},{$set: {hobby:"sing"}})
save() 方法通过传入的文档来替换已有文档。
db.users.save({_id: ObjectId("592e71029d63f20494441735"),age:24})
db.users.drop() 集合删除
