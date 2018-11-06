# 变量的结构解析赋值

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

`指定默认值`

```js
let [foo = true] = [];
foo; // true

let [x, y = 'b'] = ['a']; // x='a', y='b'
let [x, y = 'b'] = ['a', undefined]; // x='a', y='b'
```

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

# 查找字符串

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

# 字符串重复 n 次

## repeat

repeat()方法返回一个新字符串，表示将原字符串重复 n 次.

```js
'x'.repeat(3); // "xxx"
'hello'.repeat(2); // "hellohello"
'x'.repeat(0); // ""
```
