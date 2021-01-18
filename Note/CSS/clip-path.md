# 学习 clip-path

`clip-path` 还没有得到主流浏览器的支持，只是一个用于在 webkit 浏览器上一个很棒的小工具。

它的工作方式是提供一系列的`X`值和`Y`值来创建路径。当使用这些值创建一条完整路径时，就会把图像按照路径内部的尺寸进行裁剪。

## 多角形

> 创建多角形语法：`-webkit-clip-path: polygon(x-axis y-axios x-axis y-axis, ...)` 

下面的实例 `html` 部分代码都是 `<div class="box"></div>`。

```css
.box {
  width: 200px;
  height: 200px;
  background: #000 url('https://images.unsplash.com/photo-1610564413021-5c3389add1a8?ixid=MXwxMjA3fDB8MHxlZGl0b3JpYWwtZmVlZHwxNXx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60');
  background-size: cover;
  margin: 28px auto;
  -webkit-clip-path: polygon(0 100%, 50% 0, 100% 100%);
}
```

[clip-path-polygon demo](https://codepen.io/luyajiang/pen/wvzQzBR) in codepen


分析：我们以一个正方形的左上角作为原点 `x: 0, y: 0`。那么左下角就是 `x:0, y: 100%`，右下角是 `x: 100%, y:100%`，右上角是 `x: 100%, y: 0`。

所以对于上图的三角形来说，从左下角的坐标点 `x: 0, y: 100%` 开始，水平右移再垂直向上到达的左边点是 `x:50%, y:0`，再水平移到最右边最下面坐标点 `x: 100%, y:100%`。

**所有边界之外的东西都会被直接裁掉，无法显示。而元素本身仍然保持其尺寸，只是它的表示层改变了**。

## 圆形

> 创建圆形语法：`-webkit-clip-path: circle(半径 at x-axis y-axis)` 

```css
.box {
	width: 200px;
    height: 200px;
    background: #000 url('https://images.unsplash.com/photo-1610564413021-5c3389add1a8?ixid=MXwxMjA3fDB8MHxlZGl0b3JpYWwtZmVlZHwxNXx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60');
    background-size: cover;
    margin: 28px auto;
    -webkit-clip-path: circle(50% at 50% 50%);
}
```

[clip-path-circle demo](https://codepen.io/luyajiang/pen/QWKJKxb) in codepen


## 椭圆

> 创建椭圆语法：`-webkit-clip-path: ellipse(x轴半径 y轴半径 at x-axis y-axis)` 

```css
.box {
    width: 200px;
    height: 200px;
    background: #000 url('https://images.unsplash.com/photo-1610564413021-5c3389add1a8?ixid=MXwxMjA3fDB8MHxlZGl0b3JpYWwtZmVlZHwxNXx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60');
    background-size: cover;
    margin: 28px auto;
    -webkit-clip-path: ellipse(40% 20% at 50% 50%);
}
```

## Inset

> 创建Inset语法：`-webkit-clip-path: inset(top right bottom left round top-radius right-radius bottom-radius left-radius)` 

## 自定义文本框

```css
.box {
    width: 200px;
    height: 200px;
    background: #000 url('https://images.unsplash.com/photo-1610564413021-5c3389add1a8?ixid=MXwxMjA3fDB8MHxlZGl0b3JpYWwtZmVlZHwxNXx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60');
    background-size: cover;
    margin: 28px auto;
    clip-path: polygon(0% 0%, 100% 0%, 100% 75%, 75% 75%, 75% 100%, 50% 75%, 0 75%);
    -webkit-clip-path: polygon(0% 0%, 100% 0%, 100% 75%, 75% 75%, 75% 100%, 50% 75%, 0 75%);
    /*  五角星  */
    /*     -webkit-clip-path: polygon(50% 0%, 63% 38%, 100% 38%, 69% 59%, 82% 100%, 50% 75%, 18% 100%, 31% 59%, 0 38%, 37% 38%); */
}
```

[clip-path-polygon2 demo](https://codepen.io/luyajiang/pen/NWREdBO) in codepen


## 动画

```css
.box {
    width: 200px;
    height: 200px;
    background: #000 url('https://images.unsplash.com/photo-1610564413021-5c3389add1a8?ixid=MXwxMjA3fDB8MHxlZGl0b3JpYWwtZmVlZHwxNXx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60');
    background-size: cover;
    margin: 28px auto;
    -webkit-clip-path: polygon(0 20%, 0% 0%, 50% 0%, 80% 0, 100% 0%, 100% 50%, 100% 80%, 100% 100%, 50% 100%, 0% 100%, 0 80%, 0% 50%);
    transition: -webkit-clip-path 0.5s;
}
.box:hover {
    -webkit-clip-path: polygon(0% 20%, 20% 0%, 50% 30%, 80% 0%, 100% 20%, 70% 50%, 100% 80%, 80% 100%, 50% 70%, 20% 100%, 0% 80%, 30% 50%);
}
```

[clip-path-polygon-hover demo](https://codepen.io/luyajiang/pen/OJRapRr) in codepen

参考文章：

* [w3cplus clip-path](https://www.w3cplus.com/css3/using-making-sense-of-clip-path.html)
