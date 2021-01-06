## 什么是 BFC

BFC（Block Formatting Context）块级格式化上下文。具有 BFC 特性的元素可以看做是一个独立的隔绝容器，里面的元素不会影响外面的元素。

> 只会在块级和行内块触发

## BFC 的触发条件

* 根元素（html）
* float 不能为 none
* overflow 不能visible
* display 为 inline-block / table-cell / table-caption / flex / inline-flex
* position 为position 或 fixed

## BFC 特性及应用

* box 垂直方向的距离由 margin 决定，属于同一个 BFC 的两个相邻 box 的 margin 会发生重叠（应用一）
* BFC 的区域不会与 float box 发生重叠（应用二）
* 计算 BFC 的高度时，浮动元素也参与计算

##### 应用一：

```js
<div class="box"></div>
<div class="box"></div>

.box {
    width: 100px;
    height: 100px;
    background: rgb(216, 192, 233);
    margin: 70px;
}
```

上面代码运行之后，可以看出，两个盒子之间的间距只有 70px。**如果想要避免外边距的重叠，可以将其放在不同的 BFC 容器中**。这样上下间隔就是 140px 了。

```js
<div class="container">
  <p class="box"></p>
</div>
<div class="container">
  <p class="box"></p>
</div>

.container {
  overflow: hidden;
}

.container .box {
  width: 100px;
  height: 100px;
  background: rgb(216, 192, 34);
  margin: 70px;
}
```

##### 应用二：

```js
<div class="box" style="border: 1px solid #000;">
  <div style="width: 100px;height: 100px;background: #eee;float: left;"></div>
</div>
```

浮动的元素会脱离普通文档流，我们创建BFC `.box { overflow: hidden; }` 后，容器会包裹浮动元素。





[BFC codepen实战链接](https://codepen.io/luyajiang/pen/abmWzJX?editors=1100)

