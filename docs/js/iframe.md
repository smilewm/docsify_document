## iframe嵌套.html  

```js
  <iframe src="xxxx/xx.html" id="testIframe"></iframe>
  <button @click="save">提交</button>
  save(){
    if(document.getElementById('testIframe').contentWindow.wf_submit){
      document.getElementById('testIframe').contentWindow.wf_submit();
    }
  }

  // xx.html
  wf_submit(){};
```  

## iframe嵌套.vue  

```js
// vue-cli框架，嵌套同系统下的vue页面，可通过路由嵌套
<iframe src="/bfs/index.html?systemType=51#/test-iframe" ref="testIframe"></iframe>
<button @click="save">提交</button>
export default {
  data() {
    return {};
  },
  methods: {
    // 提交
    save() {
      if(this.$refs.testIframe.$el.contentWindow.wf_submit){
        this.$refs.testIframe.$el.contentWindow.wf_submit();
      }
    }
  }
}



// 路由
{
  path: '/test-iframe',
  name: 'test-iframe',
  component: resolve =>
    require(['../pages/work-flow/iframe'], resolve)
}

// iframe.vue
export default {
  data() {
    return {};
  },
  created() {
    window.wf_submit = this.wf_submit;
  },
  methods: {
    // 提交
    wf_submit() {}
  }
}
```