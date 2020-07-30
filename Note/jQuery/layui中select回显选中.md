layui 简直是个大坑啊...

layui 中 select 回显选中，option 值是遍历接口值得到的，一开始我用的方法是在 select 中 

```js
$('select[name="wrongCode"]').append('<option value="1">test</option>');
``` 

这种方法呢，可以展示出下拉框。但是无法回显数据啊！！！

最终解决方案（其中 `data.message` 就是需要回显的那个数据）：

```js
$.ajax({
    url: '/xxxxx/selectAll',
    method: 'get',
    dataType: 'json',
    success: function (res) {
        if (res.responseCode === '100000') {
            $.each(res.result, function (index,item) {
                var option = new Option(item.wrongCode, item.wrongText);
                if (item.wrongCode == data.wrongCode) {
                    option.setAttribute("selected", 'true');
                }
                $('#wrongCode').append(option);
                form.render('select');
            });   
        } else {
            message(res.message);
        }
    }
});
```