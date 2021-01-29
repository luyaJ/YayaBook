# Tree Shaking

>  `Tree shaking` 是一种通过清除多余代码方式来优化项目打包体积的技术，专业术语叫 `Dead code elimination`。

## 做了什么

`Tree shaking` 是基于 ES6 模板语法（import 和 exports），主要借助 ES6 模块的静态编译思想，在编译时就能确定模块的依赖关系，以及输入和输出的变量。

* 编译阶段利用 `ES6 Module` 判断哪些模块已经加载
* 判断哪些模块和变量未被使用或者引用，进而删除对应代码

## 作用

通过 `Tree Shaking`，Vue3 给我们带来的好处是：

* 减少程序体积（更小）
* 减少程序执行时间（更快）
* 便于将来对程序架构进行优化（更友好）

参考文章：

* [说说Vue 3.0中Treeshaking特性？举例说明一下？](https://mp.weixin.qq.com/s/3kGPcQ7xduLqAEAaWRJbgw)