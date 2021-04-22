# var、let、const

## var

在 ES5 中，顶层对象的属性和全局变量是等价的，用 `var` 声明的变量既是全局变量也是顶层变量

1、浏览器环境指的是 `window` 对象

<iframe   src="https://carbon.now.sh/embed?bg=rgba%28171%2C+184%2C+195%2C+1%29&t=seti&wt=none&l=auto&ds=true&dsyoff=20px&dsblur=68px&wc=true&wa=true&pv=56px&ph=56px&ln=false&fl=1&fm=Hack&fs=14px&lh=133%25&si=false&es=2x&wm=false&code=var%2520a%2520%253D%25205%253B%250Aconsole.log%28window.a%29%253B%2520%252F%252F%25205"   style="width: 378px; height: 222px; border:0; transform: scale(1); overflow:hidden;"   sandbox="allow-scripts allow-same-origin"> </iframe>

```js
var a = 5;
console.log(window.a); // 5
```

2、变量提升

```js
console.log(a); // undefined
var a = 5;
```

在编译阶段，编译器会将它变成以下执行：

```js
var a;
console.log(a);
a = 5;
```

3、对一个变量进行多次声明，后面声明的变量会覆盖前面的变量声明

```js
var a = 5;
var a = 8;
console.log(a); // 8
```

4、在函数中使用 `var` 声明变量时，该变量是局部的

```js
var a = 5;
function test() {
    var a = 8;
}
test();
console.log(a); // 5
```

参考文章：

* [wx](https://mp.weixin.qq.com/s/w49SXN2ceSW0ZSEH7v4oZw)