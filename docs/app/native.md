## 原生插件

框架集成了部分原生插件，具体包括：
* camera  拍照和选择图片
* app-update  app自动更新，只支持android
* app-version  app版本号获取
* call-number  拨打电话
* local-notifications 本地消息推送
* media-capture  视频录制
* File  文件操作

## 插件使用
从`providers/product/native/native.module`里面导入需要用到的插件，即可使用该插件。插件具体api参考[官网地址](https://ionicframework.com/docs/native/), 具体示例参考`demo`下面的`native`文件夹。

完整插件引入
```bash
import {CameraProvider,
  CameraOptions,
  ImagePickerOptions,
  File,
  LocalNotificationsProvider,
  CallNumberProvider,
  AppVersionProvider,
  AppUpdateProvider,
  FileOpenerProvider,
  MediaCaptureProvider,
  MediaFile, 
  CaptureError,
  CaptureVideoOptions,
  CaptureAudioOptions} from '../../../../providers/product/native/native.module';
```

**`插件使用示例--camera`**
```js
import { Component } from '@angular/core';
import {
  IonicPage,
  NavController,
  NavParams
} from 'ionic-angular';
import {
  CameraProvider
} from '../../../../providers/product/native/native.module';
import { CommonProvider } from '../../../../providers/product/common';

@IonicPage()
@Component({
  selector: 'page-camera',
  templateUrl: 'camera.html'
})
export class CameraPage {
  url: any[] = [];
  constructor(
    public navCtrl: NavController,
    public navParams: NavParams,
    private camera: CameraProvider,
    private commom: CommonProvider
  ) {}
  getPicture() {
      this.camera.getPicture().then(
      data => {
        data.forEach(enty => {
          console.log(enty.nativeURL); //file:///storage/emulated/0/Android/data/com.zeei.demo/cache/1530863186469.jpg
          console.log(enty.fullPath); ///1530863186469.jpg
          console.log(enty.toURL()); //file:///storage/emulated/0/Android/data/com.zeei.demo/cache/1530863186469.jpg
          console.log(enty.toInternalURL()); //cdvfile://localhost/temporary/1530863186469.jpg
          console.log(enty.filesystem); //temporary
          this.commom.toImgUrl(enty.toURL()).then(url => {
            this.url.push(url);
          });
        });
      },
      err => {
        console.log(err);
      }
    );
  }
}

```