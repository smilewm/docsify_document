# vue自定义组件  
> 通过Vue.use()来使用,即install的使用  

- 新建一个 .vue文件,例如login.vue

```html
// login.vue  
<template>
    <div>
        我是组件
    </div>
</template>
 
<script>
    export default {
        name: 'CLogin'
    }
</script>
 
```

- 建立js文件，在这个文件中使用install方法来全局注册该组件,例如index.js  

```js
import CLogin from './login.vue'  
const install = (Vue)=>{
    Vue.component( CLogin.name, CLogin );
}  
export default install 
```

- 在main.js中引入js并使用  

```js   
import components from './index.js'
Vue.use(components)
```

接下来便可以在页面中直接使用组件了 

```html 
<template>
    <c-login></c-login>
</template>
```
