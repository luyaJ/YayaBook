# 路由报错

写微网厅项目时，登陆成功后点击侧边的第一个导航栏，报错 `avigationDuplicated: Avoided redundant navigation to current location: `

原本我们是这样写的：

```vue
this.$router.push({ name: name })
```

修改为：

```vue
this.$router.push({ name: name }).catch(err => {})
```