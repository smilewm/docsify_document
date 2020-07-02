## 查找类下子元素  

`querySelectorAll`    `querySelector`

```js
document.getElementByClass('name').querySelectorAll('.custom')
document.getElementByClass('name').querySelectorAll('div')

document.getElementByClass('name').querySelector('.custom')
```  

## v-charts动态设置y轴坐标最大、最小值  

```js
  <template>
    ...
  </template> 
  <script>
    export default {
      const self = this;
      data(){
        return {
          chartExtends: {
            yAxis(y) {
              y = self.setYaxis(y);
              return y;
            }
          }
        }
      },
      methods: {
        setYaxis(y) {
          // 纵坐标为单坐标的时候，只需要设置y[0], 如需要左右双坐标，则遍历y
          if (y[0]) {
            y[0].min = function(value) {
              if(value.min!==null){
                if(value.min<0){
                  return 0;
                } else{
                  return value.min;
                }
              } else {
                return value.min;
              }
            };
            y[0].max = function(value) {
              if(value.max!==null){
                if(value.max<0){
                  return 0;
                } else{
                  return value.max;
                }
              } else {
                return value.max;
              }
            };
          }
          return y;
        }
      }
    }
  </script>
```

## 解决eslint中eval报错  

```js
  evil(fn){
    const Fn = Function; // 一个变量指向Function，防止有些前端编译工具报错
    return new Fn('return ' + fn);
  }
  //eval(...) 改成  this.evil(...) 使用
```
