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

### 增

1.push()

> 接收任意数量的参数，并将它们添加至数组尾部，返回数组的最新长度

```js
let arr = [];
let count = arr.push("luya", "xixi");
console.log(count) // 2
```

2.unshift()

> 在数组头部添加任意多个值，返回新的数组长度

```js
let arr = new Array();
let count = arr.unshift("luya", "xixi");
console.log(count) // 2
```

3.splice()

> 传入三个参数，分别是开始位置、0（要删除的元素数量）、插入的元素，返回空数组

```js
let arr = ["luya", "xixi", "test"];
let newArr = colors.splice(1, 0, "xiao", "ming")
console.log(arr) // ["luya", "xiao", "ming", "xixi", "test"]
console.log(newArr) // []
```



## 其他

#### 1.去除数组中重复的元素

```js
let uniqueArray = [...new Set([1, 2, 5, 5, 5, "luya", "luya", 'haha', false, false, true, true])];
// [1, 2, 5, "luya", "haha", false, true]
```