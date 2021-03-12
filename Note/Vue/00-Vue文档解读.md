# Vue官网文档学习及解读

## 1.mixin（混入）

[官方文档 - mixin](https://cn.vuejs.org/v2/guide/mixins.html)

普通情况引入组件，相当于在父组件中开辟了一块单独的空间，而 `mixins` 是在引入组件后，将组件内部的内容（如data，methods等）与父组件相应内容进行合并。

**作用：**多个组件可以共享数据和方法，在使用 mixin 的组件引入后，mixin 中的方法和属性也就并入到该组件中，可以直接使用。mixin 中的钩子函数先执行。

**用法：**

1.定义一个 `mixin.js` 文件

```js
// 定义一个混入对象
const myMixin = {
  created: function () {
    this.hello()
  },
  methods: {
    hello: function () {
      console.log('hello from mixin!')
    }
  }
}

export { myMixin }
```

2.在组件中使用 `mixin`

```js
import { myMixin } from '@/utils/mixin.js'
export default {
  mixins: [myMixin]
}
```

## 2.过滤器

过滤器可以用在两个地方：

```js
<!-- 在双花括号中 -->
{{ name | formatName }}

<!-- 在 `v-bind` 中 -->
<div v-bind:id="name | formatName"></div>
```

我们可以在一个组件的选项中定义本地的过滤器：（也可以在创建Vue实例之前全局定义过滤器）

```JavaScript
filters: {
    formatName: function(value) {
        if (!value) return ''
        return value.toUpperCase();
    }
}
```

在上面的例子中，`formatName` 过滤器函数将会收到 `name` 的值作为第一个参数。

**实战**：

```js
<!-- processStep是接口返回的字段 -->
<a-badge :text="processStep | statusFilter" />

filters: {
    statusFilter(type) {
        const statusMap = {
          '0': '待审核',
          '1': '审核不通过',
          '2': '审核通过',
          '3': '勘查通过',
          '4': '勘查不通过',
          '5': '方案确定'
        }
        return statusMap[type]
    }
}
```

如果 `processStep` 值是2，那么页面上将展示“审核通过”。
