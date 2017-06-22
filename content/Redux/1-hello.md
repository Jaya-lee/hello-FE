### Redux是什么 ？ 与React有什么关系

Redux 是一个配合 React 使用的数据流管理工具，负责组件间通信。

当然redux可以配合多种框架使用，并不仅是针对react。

### 那还需要学Redux做什么 ？

是的，在之前学React时实现组件间通信我们也可以直接用组件互相操作的形式(props传入一个方法)来实现。

在下面例子中：

通过子组件，修改父组件的 state ，然后把父组件的 state 作为所有子组件的 props 值传入各个子组件，实现了各个兄弟组件间通信。

```js
父组件
render() {
  return (
    <div>
      <div className='top clearfix'>
          <PostBody comment={this.state.all}/>
      </div>
      <div className='bottom clearfix'>
          <CommentBox num={this.handleNum}/>
      </div>
    </div>
  )
}

Search(子组价一)
handleSubmit(e){
    return this.props.num(this.state.comment.length+1)
}

Hello(子组件二)
 <div className='num comment-num'>评论{this.props.comment}</div>

```
但是这种情况只限于两两组件之间，而且操作相当麻烦。

有了Redux，我们可以任意的实现任何组件之间的通信。

jaya内心:又一个逆天的黑魔法。。。

### Redux 作者

[Dan](https://github.com/gaearon) ， Redux 之父，目前是 facebook公司 React 项目老大。

Dan是这样子说的:

>一个 React 的 props 还用不好的开发者，是不应该去学 Redux

哈哈，所以react用的比较爽的时候再学redux哦，不要急
