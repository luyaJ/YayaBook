# 学习 clip-path

`clip-path` 还没有得到主流浏览器的支持，只是一个用于在 webkit 浏览器上一个很棒的小工具。

它的工作方式是提供一系列的`X`值和`Y`值来创建路径。当使用这些值创建一条完整路径时，就会把图像按照路径内部的尺寸进行裁剪。

## 多角形

> 创建多角形语法：`-webkit-clip-path: polygon(x-axis y-axios x-axis y-axis, ...)` 

下面的实例 `html` 部分代码都是 `<div class="box"></div>`。

<iframe
  src="https://carbon.now.sh/embed?bg=rgba%28171%2C+184%2C+195%2C+1%29&t=3024-night&wt=none&l=auto&ds=true&dsyoff=20px&dsblur=68px&wc=true&wa=true&pv=56px&ph=56px&ln=false&fl=1&fm=Hack&fs=14px&lh=133%25&si=false&es=2x&wm=false&code=.box%2520%257B%250A%2520%2520width%253A%2520200px%253B%250A%2520%2520height%253A%2520200px%253B%250A%2520%2520background%253A%2520%2523000%2520url%28%27https%253A%252F%252Fimages.unsplash.com%252Fphoto-1610564413021-5c3389add1a8%253Fixid%253DMXwxMjA3fDB8MHxlZGl0b3JpYWwtZmVlZHwxNXx8fGVufDB8fHw%25253D%2526ixlib%253Drb-1.2.1%2526auto%253Dformat%2526fit%253Dcrop%2526w%253D500%2526q%253D60%27%29%253B%250A%2520%2520background-size%253A%2520cover%253B%250A%2520%2520margin%253A%252028px%2520auto%253B%250A%2520%2520-webkit-clip-path%253A%2520polygon%280%2520100%2525%252C%252050%2525%25200%252C%2520100%2525%2520100%2525%29%253B%250A%257D"
  style="width: 1024px; height: 366px; border:0; transform: scale(1); overflow:hidden;"
  sandbox="allow-scripts allow-same-origin">
</iframe>

<span>See the Pen <a href="https://codepen.io/luyajiang/pen/wvzQzBR">
  clip-path-polygon</a>
  on <a href="https://codepen.io">CodePen</a>.</span>


分析：我们以一个正方形的左上角作为原点 `x: 0, y: 0`。那么左下角就是 `x:0, y: 100%`，右下角是 `x: 100%, y:100%`，右上角是 `x: 100%, y: 0`。

所以对于上图的三角形来说，从左下角的坐标点 `x: 0, y: 100%` 开始，水平右移再垂直向上到达的左边点是 `x:50%, y:0`，再水平移到最右边最下面坐标点 `x: 100%, y:100%`。

**所有边界之外的东西都会被直接裁掉，无法显示。而元素本身仍然保持其尺寸，只是它的表示层改变了**。

## 圆形

> 创建圆形语法：`-webkit-clip-path: circle(半径 at x-axis y-axis)` 

<span>See the Pen <a href="https://codepen.io/luyajiang/pen/QWKJKxb">
  clip-path-circle</a> on <a href="https://codepen.io">CodePen</a>.</span>


## 椭圆

> 创建椭圆语法：`-webkit-clip-path: ellipse(x轴半径 y轴半径 at x-axis y-axis)` 

## Inset

> 创建Inset语法：`-webkit-clip-path: inset(top right bottom left round top-radius right-radius bottom-radius left-radius)` 

## 自定义文本框

<iframe height="265" style="width: 100%;" scrolling="no" title="clip-path-polygon2" src="https://codepen.io/luyajiang/embed/NWREdBO?height=265&theme-id=dark&default-tab=css,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/luyajiang/pen/NWREdBO'>clip-path-polygon2</a> by luyaJ
  (<a href='https://codepen.io/luyajiang'>@luyajiang</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

## 动画

<iframe height="265" style="width: 100%;" scrolling="no" title="clip-path-polygon-hover" src="https://codepen.io/luyajiang/embed/OJRapRr?height=265&theme-id=dark&default-tab=css,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/luyajiang/pen/OJRapRr'>clip-path-polygon-hover</a> by luyaJ
  (<a href='https://codepen.io/luyajiang'>@luyajiang</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>


参考文章：

* [w3cplus clip-path](https://www.w3cplus.com/css3/using-making-sense-of-clip-path.html)
