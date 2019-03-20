## 相同点

- 都是循环遍历数组中的每一项
- forEach 和 map 方法里每次执行匿名函数都支持 3 个参数，参数分别是 item（当前每一项）、index（索引值）、arr（原数组）
- 匿名函数中的 this 都是指向 window
- 只能遍历数组

## map()方法

`map定义和用法:`

- map 方法返回一个新的数组，数组中的元素为原始数组调用函数处理后的值。
- map()方法不会改变原始数组。
- map()方法不会对空数组进行检测。

```js
var arr = [0, 2, 4, 6, 8];
var str = arr.map(function(item, index, arr) {
  console.log(this); //this指向window
  return item / 2;
}, this);
console.log('原数组arr：', arr); // [0,2,4,6,8]
console.log(str); // [0,1,2,3,4]
```

## forEach()方法

- 用于调用数组的每个元素，将元素传给回调函数
- 不会对空数组调用回调函数
- 改变原数组

```js
var arr = [0, 2, 4, 6, 8];
var str = arr.forEach(function(item, index, arr) {
  console.log(this); //this指向window
  return item / 2;
}, this);
console.log('原数组arr：', arr); // [0,1,2,3,4]
console.log(str); // [0,1,2,3,4]
```
