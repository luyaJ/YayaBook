# 1.DOCTYPE是什么，作用是什么

DOCTYPE文档类型作用：告诉浏览器以哪种方式解析html。

DOCTYPE有3种类型：Strict、Transitional、Frameset，如果不制定DOCTYPE，浏览器默认使用混杂模式。

# 2.如何理解html语义化

正确使用html标签，易于阅读，利于seo，方便其他设备解析，有利于开发维护。

# 3.html标签

**分类：**

* 行级标签：`a`、`span`、`em`、`strong`、`button`、`img`、`input`、`select`、`textarea`
* 块级标签：`div`、`table`、`ul`、`ol`、`li`、`tbody`、`h1~h6`、`form`、`p`

**区别：**

* 块级元素独占一行，其宽度自动填满父元素的宽度；
* 块元素可以设置width/height属性，行内元素设置无效；
* 块元素可以设置margin/padding属性，行内元素水平方向设置会产生边距效果，竖直方向不会产生边距效果

**h5新标签：**

* `header`、`footer`、`address`、`audio`、`video`、`canvas`、`section`、`dialog`

# 4.link和@import的区别

* `link` 是html标签，`@import` 是css提供的一种方式；
* `@import` 有兼容性要求;
* `link` 引入的资源在解析html时到了这个位置就会加载，而 `@import` 引入的资源是在html解析完成后才下载；
* `link` 引入的资源种类可以是css文件，还有rel连接属性等，而 `@import` 只能引入css文件；

# 5.如何禁止页面的缩放

在 meta 中添加 `content="user-scalable=no"` 即可防止浏览器被放大。

`maximum-scale` / `minimum-scale`  控制允许用户以怎样的方式放大或缩小页面。

# 6.回流与重绘

>  回流：计算元素的布局和尺寸

当render tree 中的一部分（或全部）因为元素的规模尺寸、布局、隐藏等改变而需要重新构建，这就称为**回流**。

每个页面至少需要一次回流，就是页面第一次加载的时候，这个时候一定会发生回流，因为要构建render tree。

在回流的时候，浏览器会使渲染树中受到影响的部分失效，并重新构造这部分渲染树，完成回流后，浏览器会重新绘制受影响的部分到屏幕中，该过程称为重绘。

**重绘**：元素的外观发生了变化且不影响布局，比如 `background-color`。

**注意：**回流必将引起重绘，而重绘不一定引起回流。