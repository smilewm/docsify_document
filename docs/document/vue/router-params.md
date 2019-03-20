# vue-router 路由传参  

```js
routes: [
  {
    path: '/home',
    name: 'home',
    component: ...
  }
]
```

<strong>声明式的导航：</strong> 
```js
<router-link to="news">click to news page</router-link>

<router-link :to="{ name: 'news', params: { userId: 1111}}">click to news page</router-link>
```

<strong>编程式导航:</strong>

1.无参路由跳转:

```js
this.$router.push('home');
```  

2.带参路由跳转:

* params传递参数(类似于post请求)  

!> `注意：命名路由这种方式传递的参数，如果在目标页面刷新会出错`  

```js
this.$router.push({ name: 'home', params: { userId: 123 }}) // 传递参数

this.$route.params.userId // 接受传递的参数
```  

* query传递参数(类似于get请求)

!> `必须配合path来传递参数而不能用name`  

```js
this.$router.push({ path: '/home', query: { userId: 123 }})  

this.$route.query.userId
```  

router.js中配置路由参数

```js
routes: [{
  // 流程审核
  path: '/process-approval/:id',
  name: 'process-approval',
  component: resolve => require(['../pages/work-flow/process-approval'], resolve)
}]

this.$router.push({
  path: `/process-approval/${this.row.deployId}`
});

this.$route.param.id
```
