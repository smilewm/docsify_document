## 模块引入
对已存在的模块里面的组件进行引入，使不同的项目可以公用不同模块之间的组件及服务代码。

* 把模块加入到pages目录下，如框架示例模块`demo`
* 在`app.module.ts`中导入模块下面的`module.ts`文件，例如：import { DemoModule } from '../pages/demo/module';
* 把导入的文件加入到`@NgModule`里面的`imports`数组里面，即可完成导入。

`app.module.ts`

```js
import { CommModule } from '../module'; //框架提供的基础模块
import { DemoModule } from '../pages/demo/module'; //demo示例程序模块
@NgModule({
  declarations: [MyApp],
  imports: [
    BrowserModule,
    HttpClientModule,
    IonicModule.forRoot(MyApp, {
      backButtonText: '返回',
      iconMode: 'ios',
      mode: 'ios',
      modalEnter: 'modal-slide-in',
      modalLeave: 'modal-slide-out',
      tabsPlacement: 'bottom',
      pageTransition: 'ios-transition',
      tabsHideOnSubPages: true
    }),
    IonicStorageModule.forRoot(),
    /**
     * 模块引入到这里
     */
    CommModule,
    DemoModule
  ],
  bootstrap: [IonicApp],
  entryComponents: [MyApp],
  providers: [
    { provide: ErrorHandler, useClass: IonicErrorHandler },
    { provide: HTTP_INTERCEPTORS, useClass: InterceptorProvider, multi: true }
  ]
})
export class AppModule {}
```