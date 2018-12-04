# 结构解析赋值

## 赋值

```js
let [a, b, c] = [1, 2, 3];
// a = 1   b = 2   c = 3

let [, , third] = [1, 2, 3];
// third = 3

let [x, , y] = [1, 2, 3];
// x = 1   y = 3

let [head, ...tail] = [1, 2, 3, 4];
// head = 1     tail = [2, 3, 4]
```

## 默认值

`指定默认值`

```js
let [foo = true] = [];
foo; // true

let [x, y = 'b'] = ['a']; // x='a', y='b'
let [x, y = 'b'] = ['a', undefined]; // x='a', y='b'
```

## 对象解析

`对象的结构解析`

```js
let { foo, bar } = { foo: 'aaa', bar: 'bbb' };
foo; // "aaa"
bar; // "bbb"

let { bar, foo } = { foo: 'aaa', bar: 'bbb' };
foo; // "aaa"
bar; // "bbb"

let { baz } = { foo: 'aaa', bar: 'bbb' };
baz; // undefined
```

# 字符串

!> `都对大小写敏感`

## indexOf

返回某个指定的字符串值在字符串中`首次出现的位置`，没找到则返回`-1`。第二个参数表示`开始检索位置`，为空则从首字符开始检索

```js
string.indexOf('abc');
string.indexOf('abc', 10);
```

## includes

返回布尔值，表示是否找到了参数字符串,第二个参数表示开始检索位置

## startsWith

返回布尔值，表示茶杯上个月字符串是否在原字符串的头部,第二个参数表示开始检索位置

## endsWith

返回布尔值，表示茶杯上个月字符串是否在原字符串的尾部,第二个参数表示开始检索位置，`从后往前数`

## repeat

repeat()方法返回一个新字符串，表示将原字符串重复 n 次.

```js
'x'.repeat(3); // "xxx"
'hello'.repeat(2); // "hellohello"
'x'.repeat(0); // ""
```

> - 参数如果是小数，会被取整
> - 参数小于等于-1 或者 Infinity，会报错
> - 参数 NaN 等同于 0

# 补全

如果某个字符串不够指定长度，会在头部或尾部补全。

## padStart

用于头部补全

```js
'x'.padStart(5, 'ab'); // 'ababx'
'x'.padStart(4, 'ab'); // 'abax'
'xyzkey'.padStart(4, 'ab'); // 'xyzkey'
```

## padEnd

用于尾部补全

```js
'x'.padEnd(5, 'ab'); // 'xabab'
'x'.padEnd(4, 'ab'); // 'xaba'
```

# 模板字符串

用反引号` `` `标识

```js
`<ul>
<li>${param}</li>
</ul>`;
```

> 可嵌入变量，变量写在`${ }`中

如果大括号内部是一个字符串，将会原样输出。

```js
`Hello ${'World'}`; // "Hello World"
```

# 数值

## Number.isFinite()

用来检查一个数值是否为有限的(finite)，即不是`Infinity`。如果参数类型不是数值，一律返回 `false`

```js
Number.isFinite(15); // true
Number.isFinite(0.8); // true
Number.isFinite(NaN); // false
Number.isFinite(Infinity); // false
Number.isFinite(-Infinity); // false
Number.isFinite('foo'); // false
Number.isFinite('15'); // false
Number.isFinite(true); // false
```

## Number.isNaN()

用来检查一个值是否为`NaN`。如果参数类型不是 NaN，一律返回`false`

```js
Number.isNaN(NaN); // true
Number.isNaN(15); // false
Number.isNaN('15'); // false
Number.isNaN(true); // false
Number.isNaN(9 / NaN); // true
Number.isNaN('true' / 0); // true
Number.isNaN('true' / 'true'); // true
```

## Number.isInteger()

用来判断一个数值是否为`整数`。javascript 内部，整数和浮点数采用的是同样的存储方法，所以 25 和 25.0 被视为同一个值。如果参数不是数值，返回`false`

```js
Number.isInteger(25); // true
Number.isInteger(25.0); // true
Number.isInteger(25.1); // false
Number.isInteger(); // false
Number.isInteger(null); // false
Number.isInteger('15'); // false
Number.isInteger(true); // false
```

## Math.trunc()

用于`去除一个数的小数部分，返回整数部分`，对于非数值，内部使用 Number 方法将其先转为数值，对于空值和无法截取整数的值，返回 NaN。

```js
Math.trunc(4.1); // 4
Math.trunc(4.9); // 4
Math.trunc(-4.1); // -4
Math.trunc(-4.9); // -4
Math.trunc(-0.1234); // -0

Math.trunc('123.456'); // 123
Math.trunc(true); //1
Math.trunc(false); // 0
Math.trunc(null); // 0

Math.trunc(NaN); // NaN
Math.trunc('foo'); // NaN
Math.trunc(); // NaN
Math.trunc(undefined); // NaN
```

# 函数

## 箭头函数

```js

(params) => { ... }

```

## 参数默认值

```js
function add(x, y = 10) {
  return x + y;
}
add(10); // 20
add(10, 5); // 15
```

## rest 参数

```js
function add(...values) {
  // values为数组
}
add(2, 3, 4);
```

# 数组

## ...扩展运算符

将一个数组转为用逗号分隔的参数序列。

```js
console.log(...[1, 2, 3]); // 1,2,3
console.log(1, ...[2, 3, 4], 5); // 1,2,3,4,5
```

```js
function add(x, y) {
  return x + y;
}

const num = [4, 38];
add(...num); // 42
```

## Math.max 数组最大值

简化求出一个数组最大元素

```js
// ES5写法
Math.max.apply(null, [14, 3, 77]);

// ES6写法
Math.max(...[14, 3, 77]);
// 等同于
Math.max(14, 3, 77);
```

## 数组添加数组

通过 push 函数，将一个数组添加到另一个数组的尾部

```js
// ES5 的写法
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
Array.prototype.push.apply(arr1, arr2);

// ES6 的写法
let arr1 = [0, 1, 2];
let arr2 = [3, 4, 5];
arr1.push(...arr2);
```

## 复制数组

```js
const a1 = [1, 2];
// ES5
const a2 = a1.concat();

// ES6
const a2 = [...a1];
// 或者
const [...a2] = a1;
```

## 合并数组

```js
//都是浅拷贝
const arr1 = [1, 2];
const arr2 = [3, 4];
const arr3 = [5, 6];
// ES5 的合并
arr1.concat(arr2, arr3); // [1,2,3,4,5,6]
// ES6
const arr4 = [...arr1, ...arr2]; // [1,2,3,4]
```

## Array.from()对象转数组

用于将两类对象转为真正的数组：类似数组的对象和可遍历的对象。如果参数是一个数组，则会返回一个一模一样的新数组。

```js
let arrayLike = {
  '0': 'a',
  '1': 'b',
  '2': 'c',
  length: 3
};

// ES5的写法
var arr1 = [].slice.call(arrayLike); // ['a', 'b', 'c']

// ES6的写法
let arr2 = Array.from(arrayLike); // ['a', 'b', 'c']
```

还可以接受第二个参数，作用类似于数组的 map 方法，用来对每个元素进行处理，将处理后的值放入返回的数组。

```js
Array.from(array, x => x * x);
```

## Array.of()值转数组

用于将一组值转换为数组。用于弥补 Array()的不足，因为参数的个数不同，会导致 Array()的行为有差异

```js
Array.of(1, 2, 3); // [1, 2, 3]
Array.of(3); // [3]

Array(); // []
Array(3); // [, , ,]
Array(3, 4, 5); // [3, 4, 5]
```

## copyWithin()复制

将指定位置的成员复制到其他位置(会覆盖原有成员)，然后返回当前数组，`使用这个方法，会修改当前数组`

它接受三个参数。

`target（必需）`：从该位置开始替换数据。如果为负值，表示倒数。
`start（可选）`：从该位置开始读取数据，默认为 0。如果为负值，表示倒数。
`end（可选）`：到该位置前停止读取数据，默认等于数组长度。如果为负值，表示倒数。

```js
[1, 2, 3, 4, 5].copyWithin(0, 3); // [4, 5, 3, 4, 5]
[1, 2, 3, 4, 5].copyWithin(0, 3, 4); // [4, 2, 3, 4, 5]
[1, 2, 3, 4, 5].copyWithin(0, -2, -1); // [4, 2, 3, 4, 5]
```

## find()

找出第一个符合条件的数组成员。参数是一个回调函数，所以数组成员依次执行该回调函数，知道找出第一个返回值为 true 的成员，然后返回改成员，如果没有符合的，咋返回 undefined

```js
[1, 2, 3, 4]
  .find(n => {
    n > 3;
  }) // 4
  [(1, 2, 3, 4)].find((value, index, arr) => {
    return value > 3;
  });
// 4
```

!> 回调函数可接受三个参数，当前值、当前的位置、原数组

## findIndex()

返回第一个符合条件的数组成员的位置，如果都不符合则返回`-1`

## fill()填充

使用给定值，填充一个数组

```js
['a', 'b', 'c'].fill(7); // [7, 7, 7]
new Array(3).fill(7); // [7, 7, 7]
```

还可以接受第二个和第三个参数，用于指定填充的起始位置和结束位置

```js
[1, 2, 3, 4].fill(7, 1, 2); // [1, 7, 3, 4]
```

!> 如果填充的类型为对象，那么被赋值的是同一个内存地址的对象，而不是深拷贝对象.

```js
let arr = new Array(3).fill({ name: 'Mike' });
arr[0].name = 'Ben';
arr;
// [{name: "Ben"}, {name: "Ben"}, {name: "Ben"}]

let arr = new Array(3).fill([]);
arr[0].push(5);
arr;
// [[5], [5], [5]]
```

## includes()包含

返回一个布尔值，表示某个数组是否包含给定的值，与字符串的 includes 方法类似

```js
[1, 2, 3].includes(2); // true
```

第二个参数表示搜索的起始位置，默认为 0

```js
[(1, 2, 3)].includes(3, 3); // false
```

## flat()、flatMap()

`flat` 用于将嵌套的数组"拉平"，变成一维的数组。该方法返回一个新数组，对原数据没有影响。

```js
[1, 2, [3, 4]].flat(); // [1, 2, 3, 4]
```

!> 默认拉伸一级，传入一个整数表示拉伸的层数默认为 1，需要全部都拉伸则传入 Infinity

```js

[1, 2, [3, [4, 5, [6, 7]]]].flat(2)  // [1, 2, 3, 4, 5, [6, 7]]
[1, 2, [3, [4, 5, [6, 7]]]].flat(Infinity)  // [1, 2, 3, 4, 5, 6, 7]
// 如果原数组有空位，flat()方法会跳过空位。
[1, 2, , 4, 5].flat() // [1, 2, 4, 5]

```

`flatMap`用于对数组 map 遍历，然后对返回值组成的数组执行 flat()方法，返回一个新数组，不改变原数组。

```js
[2, 3, 4].flatMap(x => [x, x * 2]); // [2, 4, 3, 6, 4, 8]
// 相当于 [[2, 4], [3, 6], [4, 8]].flat()
```

# Set

类似于数组，但是成员的值都是唯一的，没有重复的值。

```js
const set = new Set([1, 2, 3, 4, 4]);
[...set]; // [1, 2, 3, 4]
set.size; // 4
```

> 用于数组去重 [...new Set(array)]

## 属性和方法

### 属性

- `Set.prototype.constructor`：构造函数，弄人就是 Set 函数
- `Set.prototype.size`：返回 Set 实例的成员总数

### 方法

- `add(value)`：添加某个值，返回 Set 结构本身
- `delete(value)`：删除某个值，返回布尔值表示是否删除成功
- `has(value)`：返回布尔值，表示该值是否为 Set 的成员
- `clear()`：清除所有成员

# Map

类似于对象，但是键的范围不限于字符串，各种类型的值（包括对象）都可以当作键。

size、set、get、has、delete、clear

## 互相转换

- Map 转数组

  ```js
  const myMap = new Map().set(true, 7).set({ foo: 3 }, ['abc']);
  [...myMap];
  // [ [ true, 7 ], [ { foo: 3 }, [ 'abc' ] ] ]
  ```

- 数组转 Map

```js
new Map([[true, 7], [{ foo: 3 }, ['abc']]]);
// Map {
//   true => 7,
//   Object {foo: 3} => ['abc']
// }
```

- Map 转对象

```js
function strMapToObj(strMap) {
  let obj = Object.create(null);
  for (let [k, v] of strMap) {
    obj[k] = v;
  }
  return obj;
}

const myMap = new Map().set('yes', true).set('no', false);
strMapToObj(myMap);
// { yes: true, no: false }
```

- 对象转 Map

```js
function objToStrMap(obj) {
  let strMap = new Map();
  for (let k of Object.keys(obj)) {
    strMap.set(k, obj[k]);
  }
  return strMap;
}

objToStrMap({ yes: true, no: false });
// Map {"yes" => true, "no" => false}
```

- Map 转 JSON

`一：Map的键名都是字符串，可以选择转为对象JSON`

```js
function strMapToJson(strMap) {
  return JSON.stringify(strMapToObj(strMap));
}

let myMap = new Map().set('yes', true).set('no', false);
strMapToJson(myMap);
// '{"yes":true,"no":false}'
```

`二：键名有非字符串，可以选择转为数组JSON`

```js
function mapToArrayJson(map) {
  return JSON.stringify([...map]);
}

let myMap = new Map().set(true, 7).set({ foo: 3 }, ['abc']);
mapToArrayJson(myMap);
// '[[true,7],[{"foo":3},["abc"]]]'
```

- JSON 转为 Map

`一：所有键名都是字符串`

```js
function jsonToStrMap(jsonStr) {
  return objToStrMap(JSON.parse(jsonStr));
}

jsonToStrMap('{"yes": true, "no": false}');
// Map {'yes' => true, 'no' => false}
```

`二：整个 JSON 就是一个数组，且每个数组成员本身，又是一个有两个成员的数组。这时，它可以一一对应地转为 Map`

```js
function jsonToMap(jsonStr) {
  return new Map(JSON.parse(jsonStr));
}

jsonToMap('[[true,7],[{"foo":3},["abc"]]]');
// Map {true => 7, Object {foo: 3} => ['abc']}
```

# Promise 对象

异步编程的一种解决方案。

## 特点

- 对象的状态不受外界影响  
  三种状态：`pending`(进行中)、`fulfilled`(已完成)、`rejected`(已失败)  
  只有异步操作的结果，可以决定当前是哪一种状态，其他操作无法改变这个状态

```js
  const promise = new Promise((resolve, reject) => {
    .........
    if(...){
      // 成功
      resolve();
    }else{
      // 失败
      reject();
    }
  })

  promise.then(() => {
    console.log(123);
  })
```

## then

`then` 方法包含两个参数，第一个为 `resolved`状态的回调函数，第二个参数(可选)为 `rejected` 状态的回调函数

```js
promise.then(
  () => {
    // 成功
  },
  () => {
    // 失败
  }
);
```

- `then` 方法返回的是一个新的`Promise`实例(注意:不是原来那个`Promise`实例)。因此可以采用链式写法，即`then`方法后面再调用另一个`then`方法

```js
promise
  .then(() => {
    setTimeout(console.log(123), 2000);
  })
  .then(() => {
    console.log(3333333333);
  });

// 123
// 33333333333
```

## catch

`catch`指定发生错误时的回调函数

```js
promise
  .then(() => {})
  .catch(error => {
    console.log('发生错误!', error);
  });
```

## finally

`finally`用于指定不管 Promise 对象最后状态如何，都会执行的操作。

```js
promise.then(result=>{...})
.catch(error=>{...})
.finally(()=>{---})
```

## all

`Promise.all`方法用于将多个 Promise 实例，包装成一个新的 Promise 实例。

```js
const p = Promise.all([p1, p2, p3]);
```

!> p1,p2,p3 都为 Promise 实例，
