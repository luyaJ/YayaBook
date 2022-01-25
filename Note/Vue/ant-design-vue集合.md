# ant-design-vue集锦

[官方文档](https://www.antdv.com/docs/vue/introduce-cn/)

## 一、表格

### 1.自定义表格横向滚动条样式

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

### 2.表格排序

只需要升序和降序的功能，去除取消状态。由服务器排序。

```js
data() {
  return {
	sortedInfo: null,
    saveSortedInfo: null,
    sort: 'asc' // asc正序,desc倒序
  }
}

computed: {
  columns() {
    let { sortedInfo } = this
    sortedInfo = sortedInfo || {}
    return [{
      title: '序号',
      slots: { customRender: 'index' },
      width: 80
    },
    {
      title: '登记人名',
      dataIndex: 'applyName',
      width: 100,
      ellipsis: true
    },
    {
      title: '进入工位时间',
      dataIndex: 'createTime',
      width: 170,
      sorter: true,
      sortOrder: sortedInfo.columnKey === 'createTime' && sortedInfo.order
    }];
  }
}

methods: {
  pageChange (pagination, filters, sorter) {
    this.sortedInfo = sorter
    if (sorter.order === undefined) {
      this.sortedInfo = this.saveSortedInfo
    }
    if (sorter.order === 'ascend') {
      this.saveSortedInfo = sorter
    }
    
    this.pagination = pagination
    this.getData()
  },
  getData () {
    if (!this.sortedInfo) {
      this.sortedInfo = {
        order: 'ascend',
        columnKey: 'createTime'
      }
    }
     
    this.$post('/vw-shop/pc/station/queryStationRecord', {
      site: this.searchList[0][0].value,
      workshop: this.searchList[0][1].value,
      thread: this.searchList[0][2].value,
      position: this.searchList[0][3].value,
      sort: !this.sortedInfo ? 'asc' : (this.sortedInfo.order === 'ascend' ? 'asc' : 'desc'),
      pageNo: this.pagination.current,
      pageSize: this.pagination.pageSize
    }).then(res => {
      let result = res.data
      this.dataList = result.datas
      this.pagination.total = result.pageResp.count
    })
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

#### 4.输入框不显示

```bash
<a-form-item label="业务子类型">
    <a-select
        v-model="configOrderSubTypeTemp"
        placeholder="请选择业务子类型"
        label-in-value
        :disabled="queryParam.configOrderMainType ? false : true"
        @dropdownVisibleChange="getConfigOrderSubTypeList"
        @change="handleConfigOrderSubTypeChange"
    >
    <a-select-option v-for="(item, index) in configOrderSubTypeList" :key="'sub'+index" :value="index%2==0 ? item.value+1 : item.value+2">{{item.label}}</a-select-option>
    </a-select>
</a-form-item>
```

在data中需要定义为对象，这样才可以正常显示
```bash
configOrderSubTypeTemp: { label: '', value: '' }
```

#### 5.下拉搜索

针对 `第4点：输入框不显示` 进行下拉搜索的优化

```bas
<a-select
    v-model="configOrderSubTypeTemp"
        placeholder="请选择业务子类型"
        label-in-value
        :disabled="queryParam.configOrderMainType ? false : true"
        show-search
        :getPopupContainer="(triggerNode) => triggerNode.parentNode"
        :filter-option="filterOption"
        @dropdownVisibleChange="getConfigOrderSubTypeList"
        @change="handleConfigOrderSubTypeChange"
    >
    <a-select-option v-for="(item, index) in configOrderSubTypeList" :key="'sub'+index" :value="index%2==0 ? item.value+1 : item.value+2">{{item.label}}</a-select-option>
</a-select>
```

在methods 添加一个方法：

```bash
filterOption(input, option) {
	return (option.componentOptions.children[0].text.toLowerCase().indexOf(input.toLowerCase()) >= 0 )
}
```

记住一定要写上 `filterOption` 这个方法，这样就实现了下拉框可以进行通过输入的内容进行模糊搜索。

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

## 六、树相关

### 1. 自定义树标题

注意需要使用 `scopedSlots`。

```js
getTree() {
  getAction(this.url.deviceTypeList, {}).then((res) => {
    if (res.success) {
      this.treeData[0].children = res.result
      res.result.forEach(item => {
		item.childLen = item.children ? item.children.length : 0
		item.scopedSlots = { title: 'custom'}
	  })
    }
  })
}
```

```html
<a-tree
  v-if="treeData.length"
  ref="tree"
  :defaultExpandAll="true"
  :tree-data="treeData"
  @select="onSelect"
  @rightClick="onRightClick">
  <template slot="custom" slot-scope="{title, childLen}">
    <span>{{title}} ({{childLen}})</span>
  </template>
</a-tree>
```