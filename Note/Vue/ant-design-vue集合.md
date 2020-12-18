# ant-design-vue集锦

[官方文档](https://www.antdv.com/docs/vue/introduce-cn/)

## 1.自定义表格横向滚动条样式

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

