## Vue-cli2版本：

如果接口地址都是 `/xxx/xxx`，那么配置时：

```js
proxyTable: {
  '/api': {
    target: 'http://localhost:8087', // 和后端的地址映射
    changeOrigin: true,
    pathRewrite: {
      '^/api': ''
    }
  }
}
```

## Vue-cli3版本：

```bash
module.exports = {
  devServer: {
    host: 'localhost',
    port: '8081',
    proxy: {
      '/api': {
        target: 'http://118.178.xxx.xxx:8080',
        changeOrigin: true,
        pathRewrite: {
          '^/api': ''
        }
      }
    }
  }
}
```

