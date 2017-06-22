这节通过来实现一套 RESTful API ，对文章（ post ）进行增删改查操作，从而更清楚的明白了前台和后台各自的职能，也对前几节的知识点有了更系统的掌握。

# 查，读取所有文章的 API

读操作，一般用 GET 方法，所有博客posts

API代码:

```
app.get('/posts', (req, res) => {
  console.log('GET /posts........')
  Post.find().sort({'createdAt': -1}).exec(function(err, posts) {
    if (err) return res.status(500).json({error: err.message});
    res.json({ posts })
  })
})
```

代码说明:

 API 等待客户端的 GET /posts 请求，一旦收到请求，首先打印 GET /posts ，然后去进行数据库的读取操作，读到所有的文章内容，存到 posts 变量中，然后，通过 res.json 语句，把数据以 JSON 的格式反馈给客户端，供前端开发者使用。

### 读取一篇文章时的API路由

```
 app.get('/post/:id', (req) => {
   console.log('POST /post/:id', req.params.id)
 })
 ```

前台读取:

这样就有了查数据的API,前台就可以在客户端调用了(axios.get/post)

OK,读操作是非常简单的，拿到以后我们再来对它进行操作

# 增，添加一篇博客

它的功能就是接受客户端传递的复杂 JSON 数据。增一般为post请求

服务器端接收数据，需要再专门安装一个包：

```
npm i --save body-parser
```

然后添加如下代码：

```
var bodyParser = require('body-parser');
...
app.use(bodyParser.json());
```

API代码:

```
app.post('/post', (req, res) => {
  console.log(`POST /post`, req.body)
  var post = new Post(req.body);
  post.save(function(err){
    if(err) console.log(err);
  })
} )
```
这样就可以把客户端传递过来的数据，保存到数据库了。前台用axios.post调用

这样后台会给出前台相对应的API文档:

```
POST  /post

{
  title: String,
  content: String,
  category: String
}
```

上面 POST 是请求方法，/post 是 API 路由，最后是负载数据结构。然后前端开发者要按照文档写出对应的 axios 语句来(严格匹配)

# 改，更新文章内容

在 RESTful 规范下，更新一篇博客的内容要用

```
PUT /post/:id
```
API代码:

```
app.put('/post/:id', function(req, res) {
    if (req.body.title === '') return res.status(400).json({error: '文章标题不能为空！'})
    Post.findById({_id: req.params.id}, function(err, post) {
      if (err) return res.status(500).json({error:  err.message})
      for (prop in req.body) {
        post[prop] = req.body[prop];
      }
      post.save(function(err) {
        if (err) return res.status(500).json({error: err.message})
        res.json({
          message: '文章更新成功了！'
        })
      })
    })
  })
```
前台用axios.put调用

# 删，删除一条 post

根据 RESTful 规范，删除一条 post

```
DELETE /post/:id
```

API 代码：

```
app.delete('/posts/:id', function(req, res) {
  Post.findById({_id: req.params.id}, function(err, post) {
    if (err) return res.status(500).json({error: err.message});
    post.remove(function(err){
      if (err) return res.status(500).json({error: err.message});
      res.json({ message: '文章已经删除了！' });
    });
  });
});
```
前台:axios.delete

## curl命令

当我们有了API时，在用axios调用之前我们可以先使用curl测试一下，模拟客户端，确保后台是否可用，提高工作效率。

## 查

```
curl 'http://localhost:5000/post/23423532532'
```

## 增

```
curl -H "Content-Type: application/json" -X POST -d '{"title":"jaya"}' http://localhost:5000/post
```
上面:

- -H 选项后面跟的是 HTTP 报头，设置数据格式为 json
- -d 后面跟的是负载数据( payload )

## 改

```
curl -X PUT -H 'Content-Type: application/json' -d '{"title": "newTitle"}' http://localhost:5000/post/593607542cf2f60539a17692
```
post后面是id(根据上面的API代码)

# 总结

这就是完整的一个从前台到后台操作数据的过程，前台－API文档－后台。
