## 新增服务（providers）
* 复制已有provider
* 修改文件名称及class名称
* 把新添加的provider添加到到`module.ts`文件中的`providers`对象里面

>可以参考框架中的`providers`文件夹中已有provider。

```js

import { NgModule } from '@angular/core';
import { DemoProvider } from './providers/demo';
import { DemoComponentsModule } from './components/components.module';

  @NgModule({
    providers: [DemoProvider],//providers相关模块
    exports: [DemoComponentsModule]//组件模块
  })
  export class DemoModule {}
 ```