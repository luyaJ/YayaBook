# 动态添加script标签和地址

**注意**：必须是mounted，不能是created,必须等页面加载完成才能挂载。

写一个方法：

```vue
web_script(url) {
	let scriptsArr = document.getElementsByTagName('script')
	let newArr = []
	// 获取所有的script地址
	for (var i = 0; i < scriptsArr.length; i++){ 												newArr.push(scriptsArr[i].getAttribute('src', 4))
    }
    let isFirst = true // 判断是否加载过这个script，有就不加载了
    let cdnUrl = url
    newArr.forEach(item => {
    	if (item === cdnUrl) {
    		isFirst = false
    	}
    })
    if (isFirst) {
    // 创建script标签，引入外部文件
    	let script = document.createElement('script')
    	script.type = 'text/javascript'
    	script.src = url
        document.getElementById('app').appendChild(script)
   	}
}
```

在 `mounted` 时调用：

```vue
mounted() {
	let url = 'https://webapi.amap.com/maps?v=1.4.15&key=' + store.getters.gisMapkey + '&plugin=AMap.Geocoder,AMap.Autocomplete,AMap.PlaceSearch'
	this.web_script(url)
}
```

## 拓展

`getAttribute` 的第二个参数的意义：

```bash
0：默认值。搜索属性时大小写不敏感

1：搜索属性时大小写敏感，大小和小写字母必须完全匹配。

2：返回BSTR形式的属性值？此标识对事件属性无效。

4：返回完整路径URL地址。只对URL属性有效。
```

