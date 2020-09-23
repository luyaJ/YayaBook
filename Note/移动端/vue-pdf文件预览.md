<!--
 * @FileDescription: 
 * @Author: luyaj
 * @Date: 2020-09-23 17:58:16
 * @LastEditors: luyaj
 * @LastEditTime: 2020-09-23 18:03:54
-->
H5预览pdf，查找了一些方法，最后选用 `vue-pdf`

先安装 `npm i vue-pdf --save`，这里做了分页的效果。

```js
<template>
  <div v-if="pubNoticeDetail">
    <pdf ref="pdf"
          :src="picBaseUrl + pubNoticeDetail.url"
          v-for="i in numPages"
          :key="'page' + i"
          :page="i"
    ></pdf>
  </div>
</template>

<script>
import pdf from 'vue-pdf'
export default {
  components: { pdf },
  data () {
    return {
      pdfUrl: '',
      numPages: null
    }
  },
  computed: {
    // 从上一页面拿过来的数据
    pubNoticeDetail () {
      return this.$route.params
    }
  },
  methods: {
    getNumPages () {
      let loadingTask = pdf.createLoadingTask(this.picBaseUrl + this.pubNoticeDetail.url)
      loadingTask.promise.then(pdf => {
        this.numPages = pdf.numPages
      }).catch(err => {
        this.$toast.fail('pdf加载失败:' + err)
      })
    }
  },
  mounted () {
    this.getNumPages()
  }
}
</script>
```

参考文章：[Vue PDF文件预览vue-pdf](https://www.cnblogs.com/steamed-twisted-roll/p/9648255.html)