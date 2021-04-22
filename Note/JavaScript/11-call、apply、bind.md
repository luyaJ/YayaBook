# call/apply/bind 

### 相同之处

`call()`、`apply()`、`bind()` 都是改变 `this` 的指向。

### 不同之处

* call(obj, a, b, ....)
* apply(obj, [a, b, ...])
* bind 返回的是一个新的函数，你必须调用它才会被执行

参考文章：

* [菜鸟教程](https://www.runoob.com/w3cnote/js-call-apply-bind.html)