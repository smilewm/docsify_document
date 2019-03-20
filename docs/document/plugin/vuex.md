## 简介
  
 vuex是一个专为vue.js应用程序开发的<strong>状态管理模式</strong>  
   
 大型项目使用vuex，特别是多个组件共享状态时推荐使用，简单页面不建议使用
  
## 安装  

npm install vuex --save  

import Vuex from 'vuex'

Vue.use(Vuex)  

## 核心概念  

 ### State  
  
  vuex使用单一状态树，用一个对象就包含了全部的应用层级状态，至此它便作为一个“唯一数据源”而存在

 ### Getter  

  类似于vux中的computed计算，当多个组件需要用到此计算属性时，可以在vuex中采用getter，其返回值会根据它的依赖被缓存起来，且只有当它的依赖值发生了改变才会被重新计算。 

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
          return state.todos.filter(todo => todo.done);
        },
        // 获取getter中其他计算属性
        doneTodosCount: (state,getters) => {
          return this.$store.getters.doneTodos;
        },
        // 通过方法返回 store.getters.getTodoById(2)
        getTodoById: (state) => (id) => {
          return state.todos.find(todo => todo.id === id);
        }
      }
    })
    ```     

 ### Mutation    

  更改Vuex的store中的状态的唯一方法是提交mutation。Vuex中的mutation非常类似于事件。

  ```js
    const store = new Vuex.Store({
      state: {
        count: 1
      },
      mutations: {
        increment (state) {
          // 变更状态
          state.count++
        }
      }
    });
    
    // 触发
    store.commit('increment');
  ```  

  也可以传递参数  
  ```js
    ......
    increment (state, n) {
      state.count + n
    }
    ......

    // 触发
    store.commit('increment', 10);
  ```

  对象风格的提交  
  ```js
    store.commit({
      type: 'increment',
      amount: 10
    })

    mutations: {
      increment (state, payload) {
        state.count += payload.amount
      }
    }
  ```  

!> ```mutation必须是同步函数```  
不知道什么时候回调函数实际上被调用----实质上任何在回调函数中进行的状态的改变都是不可追踪的。  

 ### Action  

  Action类似于mutation，不同在于：
  1. Action提交的是mutation，而不是直接变更状态.
  2. Action可以包含任意异步操作.  

  ```js
    const store = new Vuex.Store({
      state: {
        count: 0
      },
      mutations: {
        increment (state) {
          state.count++
        }
      },
      actions: {
        increment (context) {
          context.commit('increment')
          // 或者(ES2015常用写法)
          // increment ({ commit }) {
          //  commit('increment')
          // }
        }
      }
    });  

    // 触发  
    store.dispatch('increment')
  ```  

  可在Action中执行异步操作  
  ```js
    actions: {
      incrementAsync ({ commit }) {
        setTimeout(() => {
          commit('increment')
        }, 1000)
      }
    }
  ```
 ### Module

```js
  const moduleA = {
    state: { ... },
    mutations: { ... },
    actions: { ... },
    getters: { ... }
  }

  const moduleB = {
    state: { ... },
    mutations: { ... },
    actions: { ... }
  }

  const store = new Vuex.Store({
    modules: {
      a: moduleA,
      b: moduleB
    }
  })

  store.state.a // -> moduleA 的状态
  store.state.b // -> moduleB 的状态
```

命名空间:   
```js
  const store = new Vuex.Store({
    modules: {
      account: {
        namespaced: true,

        // 模块内容（module assets）
        state: { ... }, // 模块内的状态已经是嵌套的了，使用 `namespaced` 属性不会对其产生影响
        getters: {
          isAdmin () { ... } // -> getters['account/isAdmin']
        },
        actions: {
          login () { ... } // -> dispatch('account/login')
        },
        mutations: {
          login () { ... } // -> commit('account/login')
        },

        // 嵌套模块
        modules: {
          // 继承父模块的命名空间
          myPage: {
            state: { ... },
            getters: {
              profile () { ... } // -> getters['account/profile']
            }
          },

          // 进一步嵌套命名空间
          posts: {
            namespaced: true,

            state: { ... },
            getters: {
              popular () { ... } // -> getters['account/posts/popular']
            }
          }
        }
      }
    }
  })
```