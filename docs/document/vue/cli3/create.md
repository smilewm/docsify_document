# vue cli3

  3.0版本没有了config和build文件夹,需要修改配置，在根目录创建`vue.config.js`
 
 ## 安装
    npm install -g @vue/cli  或  yarn global add @vue/cli

## 创建项目
    vue create my-project

## 运行
    npm run serve

## 修改配置
  根目录创建`vue.config.js`后修改

  ```js 
module.exports = {
  devServer: {
    port: 8088,
    https: false, 
    open: true,
    proxy: {
      '/api': {
        target: target,
        ws: true,
        changeOrigin: true
      }
    }
  },
  outputDir: '../www', // 默认'dist'
  indexPath: '../www/index.html',
  lintOnSave: false // 是否使用eslint
  ......
};
  ```