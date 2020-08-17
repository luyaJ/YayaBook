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