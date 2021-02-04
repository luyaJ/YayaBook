# Object相关

## 对象初始化

对象初始化有3种方法：

**1.构造函数**

```js
let o = new Object();
o.name = 'luya';
o.age = 18;
```

**2.对象字面量**

```js
let o = {
    name: 'luya',
    age: 18
}
```

`{}` 和 `new Object()`，默认都是继承了 Object 对象上的 prototype。

**3.Object.create()创建**

> 语法：Object.create(proto, propertiesObject);

* 第一个参数 proto：一个对象，是新创建对象的原型对象
* 第二个参数 propertiesObject：可选

`Object.create()` 创建的对象是一个空对象，在该对象上没有继承 `Object.prototype` 原型链上的属性或者方法。

```js
let a = { x: 1 };
let b = Object.create(a);
console.log(b); // {}
console.log(b.x); // 1
console.log(b.__proto__.x); // 1
```

使用 `Object.create()` 是将对象继承到原型链上，然后可以通过对象实例的 `__proto__` 属性进行访问原型链上的属性

## Object构造函数的方法

### Object.keys()

返回一个包含所有给定对象自身可枚举属性名称的数组。

```js
let a = { name: 'luya', age: 18 }
Object.keys(a) // ["name", "age"]
```

### Object.values()

返回给定对象自身可枚举值的数组。

```js
let a = { name: 'luya', age: 18 }
Object.values(a) // ["luya", 18]
```

## 其他

通过关键字 `new` 来声明 Javascript 变量，那么该变量都会被创建为对象：

```js
let str = new String();
let num = new Number();
let bool = new Boolean();
typeof str; // "Object"
```

请避免字符串、数值或逻辑对象。他们会增加代码的复杂性并降低执行速度。

参考文章：
* [MDN - Object](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object)
* [MDN - Object.create()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/create)