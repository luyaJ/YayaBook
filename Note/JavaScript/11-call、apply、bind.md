# call/apply/bind 

### 相同之处

* `call()`、`apply()`、`bind()` 都可以改变函数的 `this` 的指向。
* 第一个参数都是 this 要指向的对象，如果没有这个参数或参数为 undefined 或 null，则默认指向全局 window。

### 不同之处

* call(obj, a, b, ....)，立即执行
* apply(obj, [a, b, ...])，立即执行
* bind 返回的是一个新的函数，你必须调用它才会被执行

参考文章：

* [菜鸟教程](https://www.runoob.com/w3cnote/js-call-apply-bind.html)