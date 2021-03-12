# ant-design-vue集锦

[官方文档](https://www.antdv.com/docs/vue/introduce-cn/)

## 一、自定义表格横向滚动条样式

```css
.ant-table-body {
  &::-webkit-scrollbar {
    width: 6px; /*高宽分别对应横竖滚动条的尺寸*/
    height: 6px;
  } 
  &::-webkit-scrollbar-thumb {
    border-radius: 6px;
    background: rgba(78, 78, 80, 0.5);
  }
  &::-webkit-scrollbar-track {
    border-radius: 5px;
    background: transparent;
  }
}
```

## 二、select

#### 1.引入

一开始实在全局文件中引入的：

```js
import { Select } from 'ant-design-vue'
const antd = {
  install: (Vue) => {
    Vue.component(Select.name, Select)
      Vue.component(Select.name, Select)
  }
}
export default antd

// 组件中使用
<a-select ref="select" v-model:value="formMarket.province" placeholder="请选择所属省">
  <a-select-option value="江苏省">江苏省</a-select-option>
</a-select>

```

会报错 `a-select-option` 说这个找不到。 尝试加了 `Vue.component(Select.Option.name, Select.Option)` 也解决不了问题。

真的是个大坑啊！！！最后在这篇 [issiue](https://github.com/vueComponent/ant-design-vue/issues/1690) 中得到启发。解决方案：

```js
// 直接在组件中引入和注册
import { Select } from 'ant-design-vue'

components: { ASelectOption: Select.Option }
```

#### 2.placeholder不显示

设置默认值 defaultValue 或者当前选中值 value 为空字符串或者 null  时，placeholder  都无法正常展示，需要设置为 undefined 才可以。

```js
formMarket: {
  province: undefined
}
```

#### 3.某个模块不存在

如果报错某个模块不存在，可能是版本问题。

12月8日安装时 `"ant-design-vue": "^2.0.0-rc.3"`，过了20天已经更新到了 `"ant-design-vue": "^2.0.0-rc.6"`。重新安装下包就好了。

## 三、表单数字校验失效问题

给 `rules` 添加 `type: 'number'`

```js
rulesSamplingTask: {
    boothId: [{ required: true, message: '请输入摊位号', trigger: 'blur', type: 'number' }],
}
```

* 日期选择框：添加 `type: Object`

## 四、自定义上传图片

上传成功，但是进度条一直loading，解决：[上传时一直loading加载的问题](https://blog.csdn.net/LittleBlackyoyoyo/article/details/104810242)

## 五、对话框

通用组件文件名 `CustomModal.vue`：

```bash
<template>
  <a-modal
    :visible="visible"
    :confirm-loading="confirmLoading"
    @ok="handleOk"
    @cancel="visible = false"
  >
    <p>123</p>
  </a-modal>
</template>

<script>
export default {
  data () {
    return {
      visible: false,
      confirmLoading: false
    }
  },
  methods: {
    open () {
      this.visible = true
    },
    handleOk () {
      this.$emit('submit')
    }
  }
}
</script>
```

在其他组件中引入上面的对话框：

```js
<template>
    // 打开弹窗的按钮
    <button @click="handleOpen"></button>
	// 引入公共弹层
    <custom-modal ref="modalForm" @submit="submitReport"></custom-modal>
</template>

<script>
export default {
	methods: {
        handleOpen () {
            this.$refs.modalForm.open();
        },
        submitReport () {
            // 弹窗按钮的点击事件
        }
    }
}
</script>
```

