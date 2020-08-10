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
  loader: 'vue-loader',
  options: vueLoaderConfig
}
```

在 `main.js` 中引用 `import './assets/style/color.less'` 