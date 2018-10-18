# ionic3

## 命令

```bash
ionic serve  启动

ionic serve -p 8888 -r 35720  --dev-logger-port 55555   打开多个

ionic serve --address 192.168.xxx.xxx  使用指定ip启动

ionic cordova run android -lc  在线连接手机调试(实时更新)

ionic cordova build android  打包(debugger)

ionic cordova build android --release --prod   打包(签名)

ionic cordova resources ios    生成图标和启动图   图标大小1024x1024   启动图  2732x2732

ionic generate page xxx 生成时自动module.ts文件
```

## 生命周期

- ### ionViewDidLoad

页面加载完成触发，这里的“加载完成”指的是页面所需的资源已经加载完成，但还没进入这个页面的状态（用户看到的还是上一个页面）

- ### ionViewWillEnter

字面意义理解就是“我要进来了”的那一刻，这个时候页面刚刚开始切换。你可以在这时对页面的数据进行预处理，这个钩子是每次都会调用的。

- ### ionViewDidEnter

当这个钩子被触发的时候，用户已经进入到新页面了（页面处于激活状态），同样也是每次都会调用。

- ### ionViewWillLeave

页面准备 (is about to) 离开时触发，这时用户刚刚触发了返回按钮或者相关的事件

- ### ionViewDidLeave

页面已经 (has finished) 离开时触发，页面处于非激活状态了

- ### ionViewWillUnload

页面中的资源即将被销毁时触发

## Angular 生命周期

!> 需要引入 OnInit

```js
import { OnInit } from '@angular/core';
```

|            钩子             |                       时间点                       |    参数     |
| :-------------------------: | :------------------------------------------------: | :---------: |
|      **`ngOnChanges`**      | 在 ngOnInit 之前，当数据绑定输入属性的值发生变化时 | ( changes ) |
|       **`ngOnInit`**        |         初始化，在第一次 ngOnChanges 之后          |     --      |
|       **`ngDoCheck`**       |              每次 Angular 变化检测时               |     --      |
|  **`ngAfterContentInit`**   |              在外部内容放到组件内之后              |     --      |
| **`ngAfterContentChecked`** |         在放到组件内的外部内容每次检查之后         |     --      |
|    **`ngAfterViewInit`**    |            在初始化组件视图和子视图之后            |     --      |
|  **`ngAfterViewChecked`**   |             在组件视图和子视图检查之后             |     --      |
|      **`ngOnDestroy`**      |            在 Angular 销毁组件/指令之前            |     --      |

## 页面构成

login 文件夹下包含`login.html`、`login.module.ts`、`login.scss`、`login.ts`

**`login.module.ts`**

```js
import { NgModule } from '@angular/core';
import { IonicPageModule } from 'ionic-angular';
import { LoginPage } from './login';
@NgModule({
  declarations: [LoginPage],
  imports: [IonicPageModule.forChild(LoginPage)]
})
export class LoginPageModule {}
```

**`login.scss`**

```css
page-login {
  div {
    margin: 10px;
  }
}
```

**`login.ts`**

```js
import { Component } from '@angular/core';
import { IonicPage, NavController, NavParams } from 'ionic-angular';

@IonicPage()
@Component({
  selector: 'page-login',
  templateUrl: 'login.html'
})
export class LoginPage {
  constructor(public navCtrl: NavController, public navParams: NavParams) {}
}
```

## 组件开发
