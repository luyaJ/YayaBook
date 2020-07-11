数组的一些简单操作：

## 创建数组

创建数组的三种方式：

#### 1.创建数组并给数组元素赋值：

```js
var arr = new Array();
arr[0] = 'luya';
arr[1] = 'xixi';
```

#### 2.直接实例化：

```js
var arr = new Array('luya', 'xixi'); // 直接把元素写在括号里
```

#### 3.隐式创建：

```js
var arr = ['luya', 'xixi']; // 语法糖
```

**注意**：

```js
console.log(arr.length); // 2
arr[3] = 'haha';
console.log(arr.length); // 4
console.log(arr[2]); // undefined
```

## 遍历数组

#### 1.for循环

使用临时变量，将长度缓存起来，避免重复获取数组长度，当数组较大的时候优化效果才会比较明显。

```js
for (i = 0, len = arr.length; i < len; i++) { }
```

#### 2.forEach循环

遍历数组中的每一项，没有返回值，对原数组没有影响，不支持 IE。

```js
arr.forEach((item, index, array) => {
  console.log(item, index);
})
```

#### 3.map循环

map 的回调函数中支持 return 返回值，不影响原数组，只是把原数组拷贝了一份。

```js
arr.map((item, index, array) => {
  // do something

  return xxx
})
```

```js
var arr = [6, 4, 17, 5];
var res = arr.map((item, index, arr) => {
  return item*10;
})
console.log(res); // [60, 40, 170, 50] 原数组拷贝了一份，并进行了修改
console.log(arr); // [6, 4, 17, 5] 原数组并未发生变化
```

#### 4.for of遍历

可以正确响应break、continue和return语句。

```js
for (var value of arr) {
  console.log(value);
}
```

#### 5.filter遍历

不会改变原始数组，返回新数组。

```js
var arr = [60, 70, 65, 80, 90];
var newArr = arr.filter(item => item > 70);
console.log(newArr); // [80, 90]
console.log(arr); // [60, 70, 65, 80, 90]
```

#### 6.every遍历

`every()` 是对数组中的每一项运行给定函数，如果该函数对每一项返回 true，则返回 false。 

```js
var arr = [1, 2, 3, 4, 5, 6];
var res = arr.every((item, index, array) => {
  return item > 3
});
console.log(res); // false
```

#### 7.some遍历

`some()` 是对数组中每一项运行指定函数，如果该函数对任一项返回 true，则返回 true。

```js
var arr = [1, 2, 3, 4, 5, 6];
var res = arr.some((item, index, array) => {
  return item > 3
});
console.log(res); // true
```

#### 8.reduce

`reduce()` 方法接收一个函数作为累加器，数组中的每一个值（从左向右）开始缩减，最终为一个值。

```js
var total = [0, 1, 2, 3].reduce((a, b) => a + b); // 6
```

reduce接受一个函数，函数有四个参数，分别是：上一次的值，当前值，当前值的索引，数组。

```js
[0, 1, 2, 3].reduce((previousValue, currentValue, index, array) => {
  return previousValue + currentValue; // 1 3 6
});
```

reduce 还有第二个参数，我们可以把这个参数作为第一次调用 callback 时的第一个参数：

```js
[0, 1, 2, 3].reduce(function(previousValue, currentValue, index, array){
  return previousValue + currentValue; // 5 5+1=6 6+2=8 8+3=11
}, 5);
```

#### 9.keys, values, entries

ES6 提供三个新的方法 -- entries(), keys() 和 values() —— 用于遍历数组。它们都返回一个遍历器对象，可以用 `for...of` 循环进行遍历，唯一的区别是 keys() 是对键名的遍历、values() 是对键值的遍历，entries() 是对键值对的遍历。

```js
for (let index of ['a', 'b'].keys()) {
  console.log(index);
}
// 0
// 1

for (let elem of ['a', 'b'].values()) {
  console.log(elem);
}
// 'a'
// 'b'

for (let [index, elem] of ['a', 'b'].entries()) {
  console.log(index, elem);
}
// 0 "a"
// 1 "b"
```

## 操作数组

```js
var arr = ['luya', 'xixi'];
```

1.添加到数组的末尾

```js
var newArrLength = arr.push('haha');
// newArrLength: 3
// arr: ["luya", "xixi", "haha"]
```

2.删除数组末尾的元素

```js
var last = arr.pop();
// last: "haha"
// arr: ["luya", "xixi"]
```

3.删除数组最前面的元素

```js
var first = arr.shift();
// first: "luya"
// arr: ["xixi"]
```

4.添加元素到数组最前面

```js
var newLength = arr.unshift("hello");
// newLength: 2
// arr: ["hello", "xixi"]
```

5.找到某个元素在数组中的索引

```js
var pos = arr.indexOf('xixi');
// pos: 1
```

6.通过索引删除某个元素或多个元素

```js
arr.push('hahaha');
// arr: ["hello", "xixi", "hahaha"]

var removedItem = arr.splice(pos, 1);
// removedItem: ["xixi"]
```

7.复制一个数组

```js
var copyArr = arr.slice();
// copyArr: ["hello", "hahaha"]
```

8.获取数组中的最后一项

```js
var arr = [0, 1, 2, 3, 4, 5, 6, 7];
var item = arr.slice(-1);
// item: [7]

var iten = arr.slice(-2);
// item: [6, 7]
```

## 其他

#### 1.去除数组中重复的元素

```js
let uniqueArray = [...new Set([1, 2, 5, 5, 5, "luya", "luya", 'haha', false, false, true, true])];
// [1, 2, 5, "luya", "haha", false, true]
```