# script标签的defer和async

[景初 - 浅谈script标签的defer和async](https://segmentfault.com/a/1190000006778717)

```bash
<script src="xxxx/xx/home/home.js" type="text/javascript" async defer></script>
```

**defer**：告诉浏览器立即下载，但延迟执行。HTML5规范要求脚本按照它们出现的先后顺序执行。

**async**：也是告诉浏览器立即下载文件，但是不保证按照它们的先后顺序执行。

