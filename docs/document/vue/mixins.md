# 混入(mixins)

## 基础概况  

是一种分发 Vue 组件中可复用功能的非常灵活的方式。混入对象可以包含任意组件选项。当组件使用混入对象时，所有混入对象的选项将混入该组件本身的选项。
  
## 怎么用  

`例子`  
 - 定义一个混入对象
```js   
  export const mixin = {
    data(){
      return {
        num: 1
      }
    },
    created(){
      this.hello();
    },
    methods: {
      hello(){
        console.log(111111111);
      }
    }
  }
```

- 把混入对象混入到当前的组件中  
```vue
  <template>
    <div>
      组件1
    </div>
  </template>

  <script>
    import {mixin} from './mixin.js';
    export default {
      mixins: [mixin]
    }
  </script>
```    

## 特点  

1、方法和参数在各组件中不共享  

  在`组件1`中对`num`进行操作  

  ```js
  <template>
      <div>
        组件1
      </div>
    </template>

    <script>
      import {mixin} from './mixin.js';
      export default {
        mixins: [mixin],
        created(){
          this.num++;
        }
      }
    </script>
  ```  
  在`组件2`中的参数`num`未进行操作  

  ```js
    <template>
      <div>
        组件2 num: {{num}}
      </div>
    </template>

    <script>
      import {mixin} from './mixin.js';
      export default {
        mixins: [mixin]
      }
    </script>
  ```  

  `组件1`中 `num` 值为 `2`  
  `组件2`中 `num` 值为 `1`  

2、值为对象的选项，如methods,components等，选项会被合并，键冲突的组件会覆盖混入对象的 

  混入对象中的方法  

  ```js   
    export const mixin = {
      data(){
        return {
          num: 1
        }
      },
      created(){
        this.hello();
      },
      methods: {
        func_one(){
          console.log(111111111);
        },
        func_two(){
          console.log(222222222);
        }
      }
    }
  ```  

  组件中的方法  

  ```js
    <template>
      <div>
        组件1 num: {{num}}
      </div>
    </template>

    <script>
      import {mixin} from './mixin.js';
      export default {
        mixins: [mixin],
        created(){
          this.func_one();
          this.func_two();
          this.func_self();
        },
        method(){
          func_one(){
            console.log(3333333333);
          },
          func_self(){
            console.log(5555555555);
          }
        }
      }
    </script>
  ```    

  打印台输出  
    3333333333  
    222222222  
    5555555555  

  
3、值为函数的选项，如created，mounted等，就会被合并调用，混如对象里的钩子函数在组件里的钩子函数之前调用
  
  混入对象函数中的console

  ```js   
    export const mixin = {
      data(){
        return {
          num: 1
        }
      },
      created(){
        console.log('from mixin');
      }
    }
  ``` 
    
  组件函数中的console  

   ```js
    <template>
      <div>
        组件1 num: {{num}}
      </div>
    </template>

    <script>
      import {mixin} from './mixin.js';
      export default {
        mixins: [mixin],
        created(){
         console.log('from self');
        }
      }
    </script>
  ``` 

  打印台输出：   
    from mixin  
    from self  
  
## 与vuex的区别  

  - `vuex`: 用来做状态管理的，里面定义的变量在每个组件中均可以使用和修改，`在任一组件中修改此变量的值之后，其他组件中此变量的值也会随之修改`。

  - `mixins`: 可以定义共用的变量，在每个组件中使用，引入组件中之后，`各个变量是相互独立的，值的修改在组件中不会相互影响`。  

## 与公用组件的区别  

  - `组件`: 在父组件中引入组件，相当于在父组件`中给出一片独立的空间供子组件使用`，然后根据props来传值，但本质上`两者是相对独立`的。  

  - `mixins`: 在引入组件之后与组件中的对象和方法合并，相当于`扩展了父组件的对象与方法`，可以理解为形成了一个新的组件。  

## mixins的使用方法和注意点  

  当混合里面包含异步请求函数，而我们又需要在组件中使用异步请求函数的返回值时，我们会取不到此返回值。如下：  
  
  ```js
  mixin中  
  methods: {
    func_one(){
      new Promise((resolve, reject) => {
        let a = 1;
        setTimeout(() => {
          resolve(a);
        }, 500)
      }).then( res => {
        return res;
      })
    }
  }
  ```

  ```js
  组件中  
  <script>
    import {myMixin} from './mixin.js';
    export default {
      mixins: [myMixin],
      mounted(){
        console.log(this.func_one(), '111111111');
      }
    }
  </script>
  ```  

  控制台输出： undefined "111111111"  

  `解决方案：不要返回结果而是直接返回异步函数`

   ```js
  mixin中  
  methods: {
    func_one(){
      let result = await new Promise((resolve, reject) => {
        setTimeout(() => {
          resolve(1);
        }, 500)
      });
      return result;
    }
  }
  ```

  ```js
  组件中  
  <script>
    import {myMixin} from './mixin.js';
    export default {
      mixins: [myMixin],
      mounted(){
        this.func_one().then(res => {
          console.log(this.func_one(), '111111111');
        })
      }
    }
  </script>
  ```    

  控制台输出： 1 "111111111"