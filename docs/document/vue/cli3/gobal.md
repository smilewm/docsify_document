# 全局引入scss
根目录`vue.config.js`中添加:

```js
css: {
  loaderOptions: {
    sass: {
      // 新版node-sass下为prependData ，旧版为data
      prependData: `@import "@/assets/scss/mixin.scss";`
    }
  }
  },
```

!> 注意： prependData引入scss文件后面的`分号` `;`，不加分号，启动项目会报错
