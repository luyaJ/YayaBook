Axios 是一个基于 promise 的 HTTP 库，可以用在浏览器和 node.js 中。[Axios 中文说明文档](https://www.kancloud.cn/yunye/axios/234845)

### 1. 拦截器

```js
// 添加请求拦截器
axios.interceptors.request.use((config) => {
  // 在发送请求之前做些什么
  return config
}, function (error) {
  // 对请求错误做些什么
  return Promise.reject(error)
})

// 添加响应拦截器
axios.interceptors.response.use((response) => {
  // 对响应数据做点什么
  return response
}, (error) => {
  // 对响应错误做点什么
  return Promise.reject(error)
})

```

### 2. 拦截器（实战）

```js
import { router } from '../router'
import axios from 'axios'
import { Message } from 'ant-design-vue'

// 请求拦截器
axios.interceptors.request.use((config) => {
  if (localStorage.token) {
    config.headers.Authorization  = localStorage.token
  }
  return config
}, (error) => {
  Message.error(error.msg)
  return Promise.reject(error)
})

// 响应拦截器
axios.interceptors.response.use((response) => {
  const data = response.data
  if (data.code !== 200) {
    Message.warning(data.msg)  
    if (data.code === 500 && data.msg === '登录状态已过期') {
      localStorage.removeItem('token')
      router.push({ name: 'Login' })
    } else if (data.code === 500 && data.msg === '令牌不能为空') {
      router.push({ name: 'Login' })
      Message.warning('请重新登录')
    } 
  } 
  return data
}, (error) => {
  Message.error(error.msg)
  return Promise.reject(error)
})
```

### 3. 请求方法的封装（实战）

```js
export function post(url, data = {}) {
  return new Promise((resolve) => {
    axios({
      method: 'post',
      url,
      data
    }).then((response) => {
      resolve(response)
    }).catch((error) => {
      // 使用resolve处理按钮的loading状态
      resolve(error)
    })
  })
}

export function get(url, params = {}) {
  return new Promise((resolve, reject) => {
    axios({
      method: 'get',
      url,
      params
    }).then((response) => {
      resolve(response)
    }).catch((error) => {
      reject(error)
    })
  })
}
```

### 4. 取消请求（实战）

项目中有一个 tab，切换方式使用的是路由，测试人员提了一个 bug -- “切换速度很快时” 会出现数据叠加显示。（内心活动：手速是有多快，我咋重现不了）。认真找到问题源头，其实不是手速问题，主要是网络环境较差时请求很慢，数据就重叠了。

解决方法：Vue 路由切换时中止前面的请求。用到 axios 的`CancelToken`。

（1）在请求和响应拦截器中加入：

```js
import store from '../store'
import axios from 'axios'

// 请求拦截器
axios.interceptors.request.use((config) => {
  config.cancelToken = new axios.CancelToken(cancel => {
    store.commit('setAxiosArr', { cancel })
  })
  return config
}, function (error) {
  return Promise.reject(error)
})

// 响应拦截器
axios.interceptors.response.use((response) => {
  let data = response.data
  return data
}, (error) => {
  if (axios.isCancel(error)) { // 路由切换 请求取消
    console.log('请求被取消了')
    return new Promise(() => {})
  } else {
    return Promise.reject(error)
  }
})
```

（2）使用 Vuex 管理 `/store/index.js`：

```js
state: {
  axiosArr: [] // 储存cancel token
},
mutations: {
  setAxiosArr: (state, cancelAjax) => {
    state.axiosArr.push(cancelAjax.cancel)
  },
  clearAxiosArr: (state) => {
    state.axiosArr.forEach(item => {
      item()
    })
    state.axiosArr = []
  }
}
```

（3）在每次路由跳转前，去取消请求：

```js
router.beforeEach((to, from, next) => {
  store.commit('clearAxiosArr') // 取消请求
  next()
})
```

在网络状态不好的情况下，或者请求本身很慢的情况下切换路由试试~，可以在控制台 Network - Status 中看到红色的 cancel。请求被中断了！完工~

### 5.formData请求格式

`multipart/form-data` 是基于 post 方法来传递数据的，并且其请求内容格式为 `Content-Type: multipart/form-data`，用来指定请求内容的数据编码格式。

```js
import axios from 'axios'

export function formData (url, formData) {
  return new Promise((resolve) => {
    let config = {
      headers: {'Content-Type': 'multipart/form-data'}
    }
    axios.post(url, formData, config).then((response) => {
      resolve(response)
    }).catch((error) => {
      resolve(error)
    })
  })
}

// 请求
let formData = new FormData()
formData.append('name', this.formGoodsCategoryAdd.name)
formData.append('parentName', this.formGoodsCategoryAdd.parentName)
this.$formData('/api/system/category/add', formData).then((response) => {
    this.loadingAdd = false
    if (response.code === 200) {
        this.showAddModal = false
        this.$Message.success('新增成功')
        this.getGoodCategoryData()
    }
})
```

