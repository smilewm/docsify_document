# 常用

## Vue中子组件中传参数给父组件中回调函数时，如果这个回调函数本身需要父组件的参数信息时怎么写？

  ```js
    <child v-for="(item, index) in items" @editFn="edit(index,arguments[0])"> </child>

    methods: {
      editFn(index,data){
          // index为child上面绑定的index， data为子组件emit触发父组件方法传过来的参数
      }
    }
  ```