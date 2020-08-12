vue + iview 搭建一个新项目，因为 iview 是基于 less 的，所以我们 vue 项目中也使用 less。

npm 安装：

```bash
npm install less less-loader -D
```

安装完成后，引入 less 出现了问题，此时需要配置 less 路径：

build -> webpack.base.conf.js 里面的 module 的 rules 内添加

```js
{
  test: /\.less$/,
  loader: 'vue-loader'
},
```

在 `main.js` 中引用 `import './assets/style/color.less'` 

### 问题

Vue 中使用 less 报错 Module build failed: TypeError: loaderContext.getResolve is not a function

**解决：**

这个错误一般都是由less-loader版本过高导致的，版本号可以在 package.json 中查看；

卸载原来的 `npm uninstall less-loader -D`

安装指定版本 `npm install less-loader@4.1.0 --D`

### less全局引入无效

less 局部引入有用，但是全局引入的时候压根不生效：

修改 build -> webpack.base.conf.js 里面的 module 内容

```js
{
  test: /\.less$/
},
```