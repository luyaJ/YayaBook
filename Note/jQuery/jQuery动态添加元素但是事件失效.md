通常，jQuery 给 HTML 元素绑定事件是这样的：

```js
$('.del-item').click(function () {
  console.log('del');
});

// or

$('del-item').on('click', function () {
  console.log('del');
});
```

但是这样的事件绑定只适用于页面内已经存在的元素。[文档中这样说的](https://api.jquery.com/on/)：

> Event handlers are bound only to the currently selected elements; they must exist at the time your code makes the call to .on()

也就是说，`del-item` 元素如果是我们后面动态添加的话，那么他的事件绑定是不会生效的。

所以我们把它委托（delegated）给 `document`：

```js
$(document).on('click', '.del-item', function () {
  console.log('del');
});
```

点击事件会冒泡，而 `document` 总是存在的，这样事件就绑定到了。同理，我们也可以将事件绑定委托给某些已存在的父节点。

[笔记来源](https://blog.zfanw.com/jquery-dynamic-insert-element-bind-event/) 写的很不错，一下就懂了。