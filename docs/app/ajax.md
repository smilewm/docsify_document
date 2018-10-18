## ajax使用

* 导入http服务，import { HttpProvider,HttpParams } from '../../../providers/product/http'; from后面的路径根据实际情况修改。
* 在页面中的构造函数（constructor）中实例化http，constructor( private http: HttpProvider) {}
* 在使用的时候实例化HttpParams；let params=new HttpParams();
* 调用`request`方法，请求数据，返回 `Observable`对象.

>params中的type取值为`get`、`post`、`form`，form为表单数据提交。

**`ajax请求示例`**
```js
import { HttpProvider,HttpParams } from '../../../providers/product/http';
@IonicPage()
@Component({
  selector: 'page-ajax',
  templateUrl: 'ajax.html'
})
export class AjaxPage {
  path: string = 'https://randomuser.me/api/';
  list: Array<Object> = [];
  constructor(public navCtrl: NavController, private http: HttpProvider) {
   this.ajax();
    
  }
  ajax(){
    let params=new HttpParams();
    params.url = this.path;
    params.params = { results: "25" };
    params.type='get';
    this.http.request(params).subscribe(data => {
      this.list = data['results'];
    });
  }
}
```