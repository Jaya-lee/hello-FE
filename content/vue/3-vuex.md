# vuex

文档:https://vuex.vuejs.org/zh-cn/

## 安装

```
npm install vuex --save
```

在一个模块化的打包系统中，您必须显式地通过 Vue.use() 来安装 Vuex：

```
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)
```
当使用全局 script 标签引用 Vuex 时，不需要以上安装过程。

## 说明

Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式,它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。这点和redux不同,redux并不只服务react,它可以运用到任何框架,包括原生.

## 书写

```
const store=new Vuex.Store({
  state:{
    count:0
  },
  mutations:{
    increment (state){
      state.count++
    }
  }
})
store.commit('increment') //提交
```
`state`是原始的state值,同redux的state

`mutations`是修改state的操作,同redux里的reducer

我们像redux里那样将store写在一个单独的文件store.js中

```
import Vue from 'vue'
import Vuex from 'vuex'
Vue.use(Vuex)

let state={
  count:0
}
let mutations={
  increment (state){
    state.count++
  }
}
const store=new Vuex.Store({
  state,
  mutations
})

export default store

```

在`main.js`里注册一下,全局可以使用store,这个操作相当于react-redux里的provider接口,这样子组件就可以通过` this.$store `访问到

其他核心概念在文档中都有非常详细的说明,大家可以按demo跑一下代码就熟练了

[Getters](https://vuex.vuejs.org/zh-cn/getters.html):可以认为是 store 的计算属性

[Mutations](https://vuex.vuejs.org/zh-cn/mutations.html):更改 Vuex 的 store 中的状态的唯一方法是提交 mutation. mutation必须是同步函数

[Actions](https://vuex.vuejs.org/zh-cn/actions.html)

Action 类似于 mutation，不同在于：(同react)

- Action 提交的是 mutation，而不是直接变更状态。
- Action 可以包含任意异步操作。

[modules](https://vuex.vuejs.org/zh-cn/modules.html):Vuex 允许我们将 store 分割成模块（module),使state不那么臃肿.
