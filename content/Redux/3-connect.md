## react-redux
redux可以配合多种框架使用，并不仅是针对react，store与react组件是没有联系的。需要react-redux绑定
```
npm i --save  react-redux
```
具体使用的两个接口：Provider connect

- Provider
```js
import {Provider} from 'react-redux'
```
Provider写在顶层　store属性的值为导出的状态树
```js
<Provider store={store}></Provider>
```
被 Provider 包括起来的组件中才能找得着 store

- connect
```js
export default connect(mapStateToProps)(PostBody)
```
connect 连接 store 和组件

### 1.mapStateToProps
#### 把 store 中的数据（一部分）映射为当前组件的 props

map 的意思是“映射”
State 指的是 store 状态树（ State Tree ），也就是 store 的实际数据
Porps 就是属性

Store 中数据很多，当前组件需要的只是一部分，那么选取工作是在 mapStateToProps 中完成的
```js
const mapStateToProps = (state) => ({
  comments: state
})
```
上面的 (state) 指的就是 Store 中的全部状态，也即是 store.getState() 可以读到的内容。

使用时可以是this.props.×××

这样state改变就是造成props改变，会重新render

### 2.mapDispathToProps
#### 把dispath方法映射为当前组件的 props

```js
const mapDispathToProps = (dispath) => ({
    add: ()=>dispath({type:'ADD',value:100})
})
```
导出时：
```js

export default connect(mapStateToProps,mapDispathToProps)(PostBody)

```
使用的时候就可以作为props来用
```js
handleSubmit(){
    this.props.add()
    //add() 方法执行，发出action
}
```
[注]:

1.这里也是返回一个对象，add是一个方法

2.多次发action时比较方便

3.不需要在组件中导入store,只需在入口中导入就可以了
