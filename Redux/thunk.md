# hello thunk

thunk:模式转换

之前我们的action对象麻烦
为了复用更改写法 action.js文件放全部action

```

let addTodo = (data='default data') => {
    return {
        type: 'ADD_TODO',
        data: data
    }
}

//触发action
store.dispatch(addTodo());
```
这样如果有多个行为触发同一个Action，只要调用一下函数 addTodo 就行，并将Action要携带的数据传递给该函数。类似 addTodo 这样的函数，称之为 Action Creator。

这样的Action Creator 返回的Action 并不是一个标准的Action。
改为
```
let addTodo = (data='default data') => {
    return {
        type: ADD_TODO,
        payload: {
            data
        }
    }
}
```
payload为一个对象



## Action Creator

Action creator是Flux的产物，用来创建Action。它是一个函数，返回值为Action对象。但是在返回action之前可以对所需的数据进行一定的处理。

Action Creator 的唯一功能就是返回一个Action供 dispatch 进行调用。

## 引入redux-thunk

[官网](https://github.com/gaearon/redux-thunk)是这样说的

>Redux Thunk middleware allows you to write action creators that return a function instead of an action. The thunk can be used to delay the dispatch of an action, or to dispatch only if a certain condition is met. The inner function receives the store methods dispatch and getState as parameters.


引用它的好处：

- 可以直接在Action Creator里运行dispath

- 最重要的是实现异步操作

ok,大概了解了一下后，我们安装来使用一下，感受它的魅力。

## 安装

```
npm i redux-thunk --save
```


[补充]:

## redux-thunk
```
npm i redux-thunk --save
```
中间件middleware

### 什么是中间件

中间件就是一个函数，对store.dispatch方法进行了改造，在发出 Action 和执行 Reducer 这两步之间，添加了其他功能。

applyMiddleware 会返回一个函数，该函数接收原来的 creatStore 作为参数，返回一个应用了 middlewares 的增强后的 creatStore。

之前只能dispath action纯对象

redux-thunk可以使dispath一个方法,这个方法有两个参数(dispath,state)

尤其是我们想要发ajax请求拿到数据时，非常需要这种中间件
