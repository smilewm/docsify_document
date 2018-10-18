## zScan 二维码扫描
扫描二维码，并且返回扫描的结果。

>结果通过自定义事件`scan:text`进行返回.

## 可配置参数

无

## 组件调用

`scan.ts`
```js
import { Component } from '@angular/core';
import { IonicPage, NavController, Events } from 'ionic-angular';

@IonicPage()
@Component({
  selector: 'page-scan',
  templateUrl: 'scan.html',
})
export class ScanPage {

  constructor(public navCtrl: NavController) {
   this.events.subscribe('scan:text', text => {
      alert('我是扫描结果：' + text);
    });
  }

}
```

`scan.html`
```html
<z-scan></z-scan>
```