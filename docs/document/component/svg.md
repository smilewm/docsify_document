## 简介 
  vue-cli构建的项目中使用svg图标

## 安装、配置  

1. 安装插件:   
    ``` js
    npm i svg-sprite-loader -S
    ```
2. 更改配置文件  
  `vue-cli2.0` build/webpack.base.conf.js
   ```js
    {
      test: /\.svg$/,
      loader: 'svg-sprite-loader',
      include: [path.resolve(__dirname, '../src/icons')],
      options: {
          //symbolId: 'icon-[name]' //这个没有生效，生效的是默认的name
      }
    }
   ```

   ```js
      {
        test: /\.(png|jpe?g|gif|svg)(\?.*)?$/,
        loader: 'url',
        exclude: [path.resolve(__dirname,'../src/icons')], //排除字体图标文件
        query: {
            limit: 10000,
            name: utils.assetsPath('img/[name].[ext]')
        }
      }
   ```

   `vue-cli3.0以上` vue.config.js  
     
    ```js
      chainWebpack: (config) => {
        config.resolve.alias
        .set('@', resolve('src'))
        config.module.rules.delete("svg");  //删除默认配置svg
        config.module
        .rule('svg-smart')
        .test(/\.svg$/)
        .include
        .add(resolve('src/icons/svg')) // svg图路径
        .end()
        .use('svg-sprite-loader')
        .loader('svg-sprite-loader')
        .options({
          symbolId: 'icon-[name]'
        })
      }
    ```

  3. 下载svg文件并放入/icons/svg/目录下  
     
    ![](./images/svg.png)  

  4. 新建公用组件components/common/SvgIcon.vue  

    ```js  
      <template> 
        <svg :class="svgClass" aria-hidden="true">
            <use :xlink:href="iconName"></use>
        </svg> 
      </template>
      <script>
        export default {
          name: "svg-icon",
          props: {
            iconClass: { type: String, required: true },
            className: { type: String }
          },
          computed: {
            iconName() {
              return `#${this.iconClass}`;
            },
            svgClass() {
              if (this.className) {
                return "svg-icon " + this.className;
              } else {
                return "svg-icon";
              }
            }
          }
        };
      </script> 
      <style scoped>
        .svg-icon {
          width: 1em;
          height: 1em;
          vertical-align: -0.15em;
          fill: currentColor;
          overflow: hidden;
        }
      </style>
    ```

  5. 新建src/icons/index.js文件

    ```js
      import Vue from 'vue'
      import SvgIcon from '../../components/common/SvgIcon'
      /* require.context("./test", false, /.test.js$/);
          这行代码就会去 test 文件夹（不包含子目录） 下面的找所有文件名以 .test.js 结尾的文件能被 require 的文件。
          更直白的说就是 我们可以通过正则匹配引入相应的文件模块。
          require.context有三个参数： 
          directory：说明需要检索的目录 
          useSubdirectories：是否检索子目录 
          regExp: 匹配文件的正则表达式 */
      //全局注册 
      Vue.component('svg-icon', SvgIcon) 
      const requireAll = requireContext => requireContext.keys().map(requireContext) 
      const req = require.context('./svg', false, /\.svg$/) 
      requireAll(req)
    ```

  6. main.js中引入组件  
    ```js  
      import './icons/index.js'
    ```

  7. 组件中应用  
    ```js        
      <svg-icon icon-class="location"></svg-icon>
      <svg-icon icon-class="search"></svg-icon>
    ```