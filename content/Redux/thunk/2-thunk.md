
### 异步操作

Action Creator 中能够使用dispath ,主要是服务异步操作

什么是异步操作(async) ?
实现异步操作的主要形式 ?
主要形式是回调函数(call back) 更为流行的是promise(axios) .
异步操作最大特点:非阻塞(no-blocking)


没有thunk之前，一旦用户触发事件，action立即发出，reducer立即执行，store立即改变，这是redux的默认工作机制。

请求API

使用curl curl http://redux-hello.haoduoshipin.com/comments

```js
//Home.js
componentWillMount(){
        axios.get('http://redux-hello.haoduoshipin.com/comments')
        .then( res =>  store.dispatch({type:'COMMENT',comments:res.data.comments}))
    }

//reducer.js
let comments =[]
        function rootReducer(state = comments,action){
            switch(action.type){
                case 'COMMENT' : return action.comments

                default : return state
            }

        }
        export default rootReducer

```
会发现render输出:两次 [],[Array[10]]
