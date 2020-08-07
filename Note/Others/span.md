# span是否换行

IBS系统里的一个bug！

```bash
<div>
	<span>应付金额</span><span>0</span>
</div>

<div>
	<span>应付金额</span>
	<span>0</span>
</div>

span { display: inline-block; width: 80px; }
```

上面这个，第一个和第二个 `div` 里的 `span`，会因为 `span` 之间是否换行，而产生差异。