---
title: Vuex
date: 2018/12/15
---

# Vuex

## 什么是Vuex？

* Vuex 是一个专门为vue.js应用程序开发的`状态管理模式`

## 状态管理模式的组成部分

* state：驱动应用的数据源
* view：以声明方式将state映射到视图
* actions：响应在view上的用户输入导致的状态变化

## state

* 类似 data 的用法 
* 获取 this.$store.state
* Vuex的状态存储是响应式，从store 实例中读取状态的最简单方法就是在计算属性中返回某个状态

## getter

* 当需要从 store 中的 state 中派生一些状态 需要用到计算属性

* 当多个组件都用到 这个 计算属性 可以使用`getter`

* getter 接收 state 作为其第一个参数

  ```js
  const store = new Vuex.Store({
    state: {
      todos: [
        { id: 1, text: '...', done: true },
        { id: 2, text: '...', done: false }
      ]
    },
    getters: {
      doneTodos: state => {
        return state.todos.filter(todo => todo.done)
      }
    }
  })
  ```

### 通过属性访问

* getter 会暴露为 `store.getters`对象，可以以属性的方式访问这些值

```js
store.getters.doneTodos  // -> [{ id: 1, text: '...', done: true }]
```

* getter 也可以接收其他 getter 作为第二个参数

```js
getters: {
  //...
  doneTodosCount: (state, getters) => {
    return getters.doneTodos.length
  }
}
```

```js
store.getters.doneTodosCount   // => 1
```

* 我们可以在任何组件使用它

```js
computed: {
  doneTodosCount() {
    return this.$store.getters.doneToDoCount
  }
}
```

### 通过方法访问

```js
getters: {
  // ...
  getTodoById: (state) => (id) => {
    return state.todos.find(todo => todo.id === id)
  }
}
```

```js
store.getters.getTodoById(2) // -> { id: 2, text: '...', done: false }
```



## mutation

* 更改 store 中的状态的唯一方法是提交`mutation`
* `mutation`类似`method`
* mutation 不能直接调用 需要用 store.commit 调用触发
* 可向 store.commit 可以体提交额外参数，即mutation的`载荷(payload)`

### 提交载荷

```js
//..
mutations: {
  increment (state, n) {
    state.count += n
  }
}
```

```js
store.commit('increment',10)
```

大多数情况下载荷是一个对象 这样可以包含多个字段并且记录的mutation会更易读：

``` js
//...
mutations: {
  increment (state,payload){
    state.conut +=  payload.amount
  }
}
```

```js
store.commit('increment',{
  amount: 10	
})
```

### 对象风格的提交方式

* 提交mutation 的另一种方式 是直接使用包含type属性的对象

* ```js
  store.commit({
      type: 'increment',
      amount: 10
  })
  ```

* 使用对象风格的提交方式，整个对象都作为载荷传给mutation函数

* ```js
  mutations: {
      increment(state,payload){
          state.count += payload.amount
      }
  }
  ```

### mutation 须遵守Vue的响应规则

* 提前在store中初始化所有所需属性

* 当需要在对象上添加新属性时
  * 使用 `Vue.set(obj, 'newProp', 123) `，或者
  * 以新对象替换老对象

```JS
state.obj = { ...state.obj, newProp: 123}
```

* mutation 必须时同步函数
* 在组件中提交mutation
  * 在组建中使用`this.$store.commit('xxx')`提交mutation

## action

* action 类似 mutation 不同在于：
  * action 提交的 mutation ，而不是直接改变状态
  * action 可以包含任意异步操作

```js
const store = new Vuex.Store({
  state: {
    count: 0
  },
  mutations: {
    increment(state) {
      state.count++
    }
  },
  actions: {
    increment (context) {
      context.commit('increment')
  }
  }
})
```

* action 函数接受一个与 store 实例具有相同的方法和属性`context`对象，因此你可以调用`context.commit`提交一个mutation
* 当多次调用`commit`的时候

```js
actions: {
  increment({ commit }) {
    commit('increment')
  }
}
```



###  分发 Action

action 通过 `store.dispatch`方法触发：

```js
store.dispatch('incremment')
```

* action 内部执行异步操作：

```js
actions: {
  incrementAsync({ commit }) {
    setTimeout(() => {
      commit('increment')
    }, 1000)
  }
}
```



* action 同样支持在何方是和对象方式进行分发

```js
store.dispatch('incrementAsync', {
  amount: 10
})
// 以对象形式分发
store.dispatch({
  type: 'incrementAsync',
  amount: 10
})
```

### 在组件中分发 Action

* 在组件中使用`this.$store.dispatch('xxx')`分发action

### 组合action

* `store.dispatch`可以处理触发的 action 的处理函数返回的Promise，并且`store.dispatch`仍旧返回Promise

  ```js
  actions: {
    actionA({ commit }) {
      return new Promise((resolve,reject) => {
        setTimeout(()=> {
            commit('someMutation')
            resolve()
        }, 1000)
      })
    }
  }
  ```

* 分发

  ```js
  store.dispatch('actionA').then(() => {
    //...
  })
  ```

* 在另外一个action中可以

  ```js
  action: {
     actionA({ commit }) {
      return new Promise((resolve,reject) => {
        setTimeout(()=> {
            commit('someMutation')
            resolve()
        }, 1000)
      })
    },
    actionB({ dispatch, commit }) {
      return dispatch('actionA').then(() => {
        commit('someOtherMUtation')
      })
    }
  }
  ```

* 利用async/await

  ```js
  // 假设 getData() 和 grtOtherData() 返回值是 Promise
  
  actions: {
    async actionA({ commit }) {
        commit('getDate', await getData())
    },
    async actionB({ dispatch, commit }) {
      await dispatch('actionA')  //等待 actionA 完成
      commit('getOtherData', await getOtherData())
    }
  }
  ```

  