## 新增组件
* 复制已有组件目录
* 修改文件名称及组件名称
* 把新添加的组件添加到`components.module.ts`文件里面
* 把`components.module.ts`文件添加到`module.ts`文件中的`exports`对象里面

>可以参考框架中的`components`文件夹中已有组件。

`components.module.ts`

```js
import { NgModule } from '@angular/core';
import { ZScanComponent } from './z-scan/z-scan';
//引入ionic-angular
import { IonicModule } from 'ionic-angular';
import { ZTabsComponent } from './z-tabs/z-tabs';
import { ZGisComponent } from './z-gis/z-gis';
import { ZLoginComponent } from './z-login/z-login';
@NgModule({
	declarations: [ZScanComponent,
    ZTabsComponent,
    ZGisComponent,
    ZLoginComponent],
	imports: [
		IonicModule
	],
	exports: [ZScanComponent,
    ZTabsComponent,
    ZGisComponent,
    ZLoginComponent]
})
export class CommonComponentsModule {}
```