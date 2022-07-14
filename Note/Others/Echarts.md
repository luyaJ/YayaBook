# Echarts相关

## xAxis

### x轴文字过多

[参考链接](https://blog.csdn.net/suhui1995/article/details/74231671)

优化：改为多行展示

```bash
axisLabel :{
    textStyle: {
    	color: '#333333', 
    },
    formatter: function(value) {
        var ret = ""; //拼接加\n返回的类目项
        var maxLength = 8; // 每项显示文字个数
        var valLength = value.length;// X轴类目项的文字个数
        var rowN = Math.ceil(valLength / maxLength); // 类目项需要换行的行数
        if (rowN > 1) { // 如果类目项的文字大于8,
            for (var i = 0; i < rowN; i++) {
                var temp = ""; // 每次截取的字符串
                var start = i * maxLength; // 开始截取的位置
                var end = start + maxLength; // 结束截取的位置
                // 这里也可以加一个是否是最后一行的判断，但是不加也没有影响，那就不加吧
                temp = value.substring(start, end) + "\n";
                ret += temp; // 凭借最终的字符串
            }
            return ret;
        } else {
        	return value;
        }
    }
}
```



