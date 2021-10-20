# vue中不错的plugin

## vue-photo-preview

此插件用于 vue 里查看大图。

**problem：**

```bash
<img 
	v-for="(img, index) in dangerousPics.split(',')"
	:src="API_BASE_URL + img"
	:preview="Number(i)"
	:key="'img' + index"
/>
```

`dangerousPics` 是异步获取的数据，获取数据后需要调用`this.$previewRefresh();` 刷新重置一下，否则不生效。