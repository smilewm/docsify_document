## 静态资源
  1. 静态资源(大图、公用js等)放在`public`中，`绝对路径`引用 '/images/logo.png'

  2. `src/assets`中的文件引用，需要采用`相对路径`

    ```
    <template>
      <div>
        1.<img src="~@/assets/logo.png" alt="">
        2.<img :src="img" alt="">
        3. <div class="box imgurl"></div>
        4. <div class="box" :style="{background: 'url(' + img + ')' }"></div>
      </div>
    </template>
    <script>
    export default {
      data(){
        return {
          img:require('@/assets/logo.png')
        }
      }
    }
    </script>

    <style scoped>
    .box{
      height: 200px;
      width: 200px;
      display: inline-block;
    }
    .imgurl{
    background: url('~@/assets/logo.png');
    }
    </style>
    ```

    > `1、3 只能使用 ~@/assets/logo.png`  
      `2、4 只能使用 @/assets/logo.png`

    ## require

    !> 前端es6 require动态引入图片报错Error: Cannot find module "."或者"其他东西"

    1. 直接静态写死是不会报错误的:  
    ```js
      let imgUrl = require('../images/a.png');
    ```

    2. 但是如果尝试着:  
    ```js
    var imgUrl = "../images/b.jpg";
    let img = require(imgUrl);
    或者
    require(`../../assets/images/${showAllExpended?'unfold':'up'}.png`
    ```

   则会报错`Error: Cannot find module`


  **正确写法:**  
  ```js
    var imgUrl = "b.jpeg";    
    let img = require('../images/'+imgUrl);
  ```