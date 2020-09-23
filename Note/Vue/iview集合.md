<!--
 * @FileDescription: iview集合
 * @Author: luyaj
 * @Date: 2020-09-23 17:51:53
 * @LastEditors: luyaj
 * @LastEditTime: 2020-09-23 17:56:59
-->
## iview常用组件清空技巧

* 清空 DatePicker 和 TimePicker 组件: `this.$refs.dom.handleClear()`
* 清空 Select 组件: `this.$refs.dom.clearSingleSelect()`
* 清空 Table 组件: `this.$refs.dom.selectAll(false)`
* 清空 Input 组件: 直接将绑定的值置为空
* 清空 Form 组件: `this.$refs[name].resetFields()`
