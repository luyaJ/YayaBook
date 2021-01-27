<!--
 * @FileDescription: 
 * @Author: luyaj
 * @Date: 2021-01-27 11:13:14
 * @LastEditors: luyaj
 * @LastEditTime: 2021-01-27 12:00:07
-->
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



