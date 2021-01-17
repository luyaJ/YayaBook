# ElementUi 集合

## 一、在表格中使用switch组件

直接在表格中添加 `switch` 组件时，左右切换不了。需要添加 `<template slot-scope="scope"></template>`

```js
<el-table-column label="状态">
    <template slot-scope="scope">
        <el-switch
    v-model="scope.row.status"
active-text="启用"
inactive-text="停用"
:active-value="1"
:inactive-value="0"
@change="changeStatus(scope.row.status, scope.row.id)">
    </el-switch>
</template>
</el-table-column>
```

