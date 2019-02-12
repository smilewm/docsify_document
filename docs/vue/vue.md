# 官网

https://cn.vuejs.org/

## vue 创建(老版本)

- npm install -g vue-cli 全局安装脚手架

- vue init webpack `<your project>` 初始化项目

- npm install vuex -s 安装各个插件，如 vuex

- npm run dev 启动项目

- npm run build 打包项目

## vue 创建(新版本)

- npm install -g @vue/cil 老版本的为 vue-cil

- vue create `<your project>` 创建项目

- vue add vuex 安装各个插件，如 vuex

- vue serve 启动

- vue build 打包

## 修改端口号

`config/index.js` 将默认的端口号`8080` 改成自己需要的

## sass 安装与使用

```js
npm install -d sass-loader node-sass

<style lang="scss">
 $color:red;
</style>
```

## vue自定义组件  
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
