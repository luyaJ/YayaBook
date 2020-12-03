## 为什么要用？

内嵌公众号的H5项目，每次有bug了很难第一时间定位到问题在哪里，费时费脑。

工具：
1. 用微信开发者工具大部分问题还是可以重现，并且修改的（仍然不够方便）
2. 使用 vconsole，鹅厂出品。和PC端的控制台一样使用。（唯一一点，每次想看storage里的数据时，都会卡很久，是否是设备问题，待验证）

**注意:**
vconsole 这个插件源码里面是依赖 html dom api 来实现的，如果你所使用的环境不支持 dom，与原有浏览器内核有差异，可能无法使用。

## 如何引入和使用？

[vconsole官方源代码地址](https://github.com/Tencent/vConsole/blob/dev/README_CN.md)

1.使用 cdn 方式引入，[所有版本地址](https://www.bootcdn.cn/vConsole/)，在 `<head>` 中加入以下代码

```js
<script src="https://cdn.bootcss.com/vConsole/3.3.4/vconsole.min.js"></script>
<script>
  // 初始化
  var vConsole = new VConsole();
  console.log('Hello world');
</script>
```

2.使用 es6 webpack 引入

```js
npm install vconsole
// 或者
cnpm install vconsole
// 或者
yarn add vconsole
```

在 Vue 项目的 `main.js` 引入并使用：

```js
import VConsole from 'vconsole'
Vue.use(new VConsole())
```

## 根据环境区分

在 `main.js` 中加入：

```js
if (process.env.ENV_CONFIG === 'test') { // 只在测试环境调用
  Vue.use(new VConsole())
}
```
