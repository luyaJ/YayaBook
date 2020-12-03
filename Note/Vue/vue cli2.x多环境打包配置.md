vue2.x 项目自动构建会有 dev 和 prod 环境。但是实际项目中，测试环境和正式环境的服务器地址、接口地址往往不一样，所以需要再添加一个 test 测试环境。

## vue cli2.x的配置

安装 `cross-env`:

```js
npm install cross-env --save-dev
```

**1. `config` 目录下复制 `prod.env.js`，修改名为 `test.env.js`**

prod.env.js:
```js
'use strict'
module.exports = {
  NODE_ENV: '"production"',
  ENV_CONFIG: '"prod"',
  API_ROOT: '"http://prod.api.com"'
}
```

test.env.js:
```js
'use strict'
module.exports = {
  NODE_ENV: '"production"',
  ENV_CONFIG: '"test"',
  API_ROOT: '"http://test.api.com"'
}
```

**2. 修改 `build/webpack.prod.conf.js`**

```js
const envConfigMap = {
  'prod': require('../config/prod.env'),
  'test': require('../config/test.env')
}

const env = envConfigMap[process.env.ENV_CONFIG] || require('../config/prod.env')
```

**3. 修改 `build/build.js` 添加打包环境提示**

```js
// 这一步非必须
const spinner = ora('正在打包...' + process.env.ENV_CONFIG + '环境')
```

**4. 修改 `package.json` 中的脚本命令**

```js
// "build": "node build/build.js"  // 原代码
"build": "cross-env ENV_CONFIG=prod node build/build.js",
"build--test": "cross-env ENV_CONFIG=test node build/build.js"
```

**5. 运行命令打包**

```js
npm run build // 正式环境
npm run build--test // 测试环境
```

参考文章：[vue cli2.x及3.x多环境打包配置](https://www.dazhuanlan.com/2020/03/20/5e7460885a700/) 写的清晰易懂