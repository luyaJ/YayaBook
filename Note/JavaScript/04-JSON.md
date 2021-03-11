JSON（JavaScript Object Notation）是一种简单的数据格式。

在数据传输流程中，json 是以字符串的形式传递的。而 javascript 操作的是 json 对象。所以，json 对象和 json 字符串之间的相互转换是关键。

```bash
var str = '{ "key": "value" }';  // json字符串
var o = { "key": "value" };  // json对象 
```

## JSON字符串转化为JSON对象

通过 JSON.parse() 方法解析。

```js
var str = '{ "key": "value", "jian": "zhi" }';
var obj = JSON.parse(str);

obj  // {key: "value", jian: "zhi"}
obj.key  // "value"
obj.jian  // "zhi"
```

## JSON对象转化为JSON字符串

通过 JSON.stringify() 方法解析。

```js
var json = '{ "key": "value", "jian": "zhi" }';
var obj = JSON.parse(json);

var str = JSON.stringify(obj);

str  // "{"key":"value","jian":"zhi"}"
```

## 格式化JSON代码

我们不常用的 `JSON.stringify` 的一个功能，就是他可以格式化输出。

stringify 方法有三个参数：`value`，`replacer` 和 `space`。其中，后两个是可选参数。要缩进 JSON，必须使用 `space` 参数。

```js
var json = { name: "John", age: 23 };
console.log(JSON.stringify(json, null, '\t'));

>>>
{
	"name": "John",
	"age": 23
}
```

## 请求后端返回数据得到[object object]

使用 `JSON.stringify()` 将 JavaScript 对象转化成 json 字符串。