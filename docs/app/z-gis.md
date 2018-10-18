## zGis 地图

基础地图部分

![](../_images/app/app-gis.png)

## 可配置参数

|           参数            |       说明       |   类型    | 是否必须 | 可选值 | 默认值 |
| :-----------------------: | :--------------: | :-------: | :------: | :----: | :----: |
| **`showCurrentPosition`** | 是否定位当前位置 | `Boolean` |   `N`    |  `--`  | `true` |

## 组件调用

`gis.ts`

```js
import { Component } from '@angular/core';
import { IonicPage, NavController, NavParams } from 'ionic-angular';


@IonicPage()
@Component({
  selector: 'page-gis',
  templateUrl: 'gis.html',
})
export class gisPage {
  showCurrentPosition:Boolean=true;
  constructor(public navCtrl: NavController, public navParams: NavParams) {

  }
}
```

`gis.html`

```js
<z-gis [showCurrentPosition]='showCurrentPosition'></z-gis>
```
