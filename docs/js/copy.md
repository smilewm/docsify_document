## 原理

`浅度复制：`js 存储对象都是存地址的，简单复制数组或对象，指向的都是同一内存地址，改变任何一个时，都会改变。  
`深度复制：`不仅将各个属性、值逐个复制出去，而且将地址重新指引，改变值相互将不影响。

## 浅拷贝示例

```js
//对象复制
var a = { name: 123 };
var b = Object.assign(a, {});
console.log(b.name); // 123
b.name = 444;
console.log(a.name); // 444
```

```js
//数组复制
var a = [1, 2, 3];
var b = a;
console.log(b); // [1,2,3]
b[0] = 444;
console.log(a); // [444,2,3]
```

## 深度拷贝

`方法一`

```js
function deepClone(origin, target) {
  var target = target || {};
  for (var prop in target) {
    if (target.hasOwnProperty(prop)) {
      if (target[prop] !== null && typeof target[prop] === 'object') {
        origin[prop] =
          Object.prototype.toString.call(target[prop]) === '[object Array]'
            ? []
            : {};
        deepClone(origin[prop], target[prop]);
      } else {
        origin[prop] = target[prop];
      }
    }
  }
}
```

`方法二`
使用 JSON.stringify 进行序列化，JSON.parse 进行反序列化，实现"偷懒版"的深复制.

```js
var a = { name: 123 };
var b = JSON.parse(JSON.stringify(a));
b.name = 333;
console.log(a); // {name:123}
console.log(b); // {name:333}
```

## 深度拷贝示例

```js
var obj1 = { name: 123 };
var obj2 = { age: 23 };
deepClone(obj1, obj2);
obj1.age = 33;
console.log(obj1); // {name:123,age:33}
console.log(obj2); // {age:23}
```
