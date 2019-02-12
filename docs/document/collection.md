# 部分插件使用

## axios
> ajax请求，用于向后台请求数据  

```js
npm install axios -s  

// main.js中  
import axios from 'axios'  
Vue.prototype.$ajax = axios   

// 组件中使用  
this.$ajax.get('.api').then(res=>{...})
```
