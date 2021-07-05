# 路由报错

## 报错1

写微网厅项目时，登陆成功后点击侧边的第一个导航栏，报错 `avigationDuplicated: Avoided redundant navigation to current location: `

原本我们是这样写的：

```vue
this.$router.push({ name: name })
```

修改为：

```vue
this.$router.push({ name: name }).catch(err => {})
```

## 报错2

> in ./src/router/router.js Syntax Error: Unexpected token , component: () => import('@/components/Login') 

这就需要 babel 的插件了，vue-route r官网上有一段提示：

如果您使用的是 Babel，你将需要添加 syntax-dynamic-import 插件，才能使 Babel 可以正确地解析语法。

```bash
npm install babel-plugin-syntax-dynamic-import --save-dev
```

再修改 webpack 的 js 的 loader 部分：

```bash
{
    test: /\.js$/,
    loader: 'babel-loader',
    options:{
    	plugins:['syntax-dynamic-import']
    }
}
```

这样就解决了。

# 路由懒加载

为了实现更好的客户体验，首屏组件加载速度更快一些，解决白屏问题，建议使用路由懒加载。

> 懒加载：简单来说就是延迟加载或按需加载，即在需要的时候进行加载。

### 1. 未使用懒加载的路由：

```js
import Home from '@/components/Home'

export const router = [
  {
    path: '/',
    name: 'Home',
    component: Home
  }

```

### 2. Vue异步组件实现懒加载：

```js
export const router = [
  {
    path: '/',
    name: 'Home',
    component: resolve => (require(['@/components/Home'], resolve))
  }
]
```

### 3. ES实现懒加载：（常用方法）

```js
const Home = () => import('@/components/Home')

export const router = [
  {
    path: '/',
    name: 'Home',
    component: Home
    // component: () => import('@/components/Home')
  }
]
```
