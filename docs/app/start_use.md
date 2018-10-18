## 前序准备

你需要在本地安装 [node](http://nodejs.org/) 和 SVN（公司源代码管理软件）。开发框架的技术栈基于 ionic3、angular4、Typescript，提前了解和学习这些知识会对使用本框架有很大的帮助。

## 目录结构

    |--resources                  // 图标、启动页资源图片
    |--src                        // 源代码
    |----app                      // 入口文件
    |----assets                   // 主题、字体等静态资源
    |----components               // 全局公用组件
    |----providers                // 全局服务
    |----pages                    // 页面
    |------demo                   // 项目目录，开发人员主要关注目录。
    |--------components           // 项目组件目录, 如果有组件只在项目中使用，则存放在该目录下
    |--------providers            // 项目服务
    |--------assets               // 主题、字体等静态资源
    |--------pages                // 项目页面
    |--theme                      // 主题文件
    |--index.html                 // 主入口文件
    |--module.ts                  // 模块加载文件
    |--tslint.json                // tslint 配置项
    |--package.json               // package.json

## 安装

把前端框架代码通过 SVN 下载到本地目录，然后进入到代码目录。

![](../_images/app/app-svn.png)

打开 CMD 窗口，进入到该代码目录，执行以下命令。

```bash
#安装ionic
npm install -g ionic@3.20.0

#安装cordova
npm install -g cordova@8.0.0

#安装依赖
npm install

#启动一个带热重载服务，自动打开浏览器查看运行效果
ionic serve
```

**`ionic serve`**命令启动完成后会自动打开浏览器访问 http://localhost:8100 ,你看到下面的页面就代表成功了。
