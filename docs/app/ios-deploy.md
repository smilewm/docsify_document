# Ios 构建

# 登录开发者

- 登录 apple 官网[https://developer.apple.cpm](https://developer.apple.cpm)

- 点击 Account,登录 apple 开发者账号

![](../_images/app/app-ios1.png)

![](../_images/app/app-ios2.png)

- 进入 apple 配置页面，进行证书、ids 配置

![](../_images/app/app-ios3.png)

# IDs 配置

## 每个项目都有自己的唯一 ID，不能共用

- 点击左侧菜单 APP IDs,进入 ids 配置页面，点击添加按钮，进入新增页面，填写信息  
  ![](../_images/app/app-ios4.png)

  `新增页面：`

  ![](../_images/app/app-ios5.png)

  - `Name`:用来描述 App ID 的,最好是项目名称，不能使用中文

  - `Boundle ID`:是 App ID 的后缀，需与项目文件 config.xml 中的 id 对应

  - `App Services`:默认会选择 2 项，不能修改，其他项根据自己需要的服务进行勾选

  点击 `Continue` 确认，完成 IDs 配置。

# CSR 生成

## 苹果 app 通过 xcode 打包发布，需要证书方可。

- 首先进入`钥匙串访问` (两种方式都可)

  ![](../_images/app/app-ios6.png)

  ### `或者`

  ![](../_images/app/app-ios7.png)

- 进入后，点击左上角`钥匙串访问`，然后选择`证书助手`中的`从证书颁发机构请求证书...`

  ![](../_images/app/app-ios8.png)

* 填写信息，邮件地址可随意填写，然后勾选`存储到磁盘`，点击`继续`将证书保存到本地磁盘即可.

  ![](../_images/app/app-ios9.png)

# 证书 配置

回到 apple 网页配置部分，对证书进行配置

- 选择证书`Certificates`下的`All`，点击`+`进入新增页面

![](../_images/app/app-ios10.png)

- 选择开发模式下的`In-House and Ad Hoc`然后点击底部的`Continue`进入下一步

![](../_images/app/app-ios11.png)

- 进入提示页面，直接点击`Continue`即可，来到生成证书部分，点击`Choose File...`进行证书上传，然后点击`Continue`回到主界面

  ![](../_images/app/app-ios12.png)

# 证书 安装

证书配置完成，需要进行安装方可正式生效

点击证书列表，在展开的信息列里面点击`DownLoad`进行下载，在下载管理器里面，`双击`下载好的证书即可

![](../_images/app/app-ios13.png)

![](../_images/app/app-ios14.png)

![](../_images/app/app-ios15.png)

# Devices 添加

!> `注意：非企业级苹果开发者账号，在不上传 app-store 情况下，需要将设备添加到配置里面方可安装`

!> `企业级账号不需要进行该项配置，可跳过`

![](../_images/app/app-ios16.png)

`只需填写 Name 和 UDID 项即可，UDID 为手机唯一识别码，具体如何查看自行百度`

![](../_images/app/app-ios17.png)

# 添加 ios platform

!> 执行命令过程中可能会提示权限不够，需要进行终端授权，在项目目录终端中执行`sudo chown -v -R -L zeei .`进行授权

```bash
# 添加 ios platform
sudo ionic cordova platform add ios
```

> 平台添加成功后，框架集成的 cordova 插件也会同步安装，项目中可以用已经集成的原生插件。

# 桌面图标、启动图制作

> 桌面图标 `icon.png` 尺寸 `1024x1024`。 启动图 `splash.png` 尺寸 `2732x2732`

将图片放于项目目录 `resources` 文件夹下，其中的 ios、android 为执行命令后生成，生成不同分辨率屏幕下的图标和启动图

```bash
ionic cordova resources ios  命令
```

![](../_images/app/app-ios18.png)

# 打包

```bash
sudo ionic cordova build ios
```

> 如果看到 Build Success! 说明你已经编译成功了.

编译完成后，`双击`编译生成的文件，进入 `xcode` 打包部分

![](../_images/app/app-ios18.png)

- Version、Build 为打包的版本号
- 选择对应的证书，不能乱选，否则无法打包，或者勾选`Automatically manage signing`让其自动配置
- 打包前，选择`Generic IOS Device`，打包不能将苹果设备插在电脑上，否则打包失败。

![](../_images/app/app-ios20.png)

点击`Product`选择`Archive...`进行打包，等待打包完成

![](../_images/app/app-ios21.png)

打包完成进入导出页面，点击`Export`进行导出

![](../_images/app/app-ios22.png)

选择一种分配方式：企业级账号现在第三个，个人账号选择第二个

![](../_images/app/app-ios23.png)

需要 manifest.plist 配置文件则勾选

![](../_images/app/app-ios24.png)

选择对应的证书

![](../_images/app/app-ios25.png)

导出，选择导出路径完成导出

![](../_images/app/app-ios26.png)

# 解决异常错误

在执行命令运行代码、编译过程中出现的部分问题给与解决方案

- 执行 ionic 命令，提示无权限，需要使用管理员账号，此时在命令前加上`sudo`即可，然后输入密码

```bash
sudo ionic cordova build ios
```

- 编译失败提示如下错误

![](../_images/app/app-ios27.png)

![](../_images/app/app-ios28.png)

![](../_images/app/app-ios29.png)

![](../_images/app/app-ios30.png)
