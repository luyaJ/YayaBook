# app内嵌H5相关问题

## H5支付

[微信官方支付文档](https://pay.weixin.qq.com/wiki/doc/apiv3/wxpay/pages/index.shtml)

需求：H5 内嵌在 APP 内，H5有充值缴费功能，H5会唤起微信进行支付，支付完成后返回APP。

```js
doRecharge () {
  if (this.totalAmount || this.customMoney) {
    this.disabledRecharge = true
    this.$post('/wwt/pay/doRecharge', {
      accountNo: window.localStorage.accountNo,
      customerId: this.customerId,
      supplierId: window.localStorage.supplierId,
      totalAmount: this.totalAmount || this.customMoney,
      userName: window.localStorage.userName,
      ip: returnCitySN['cip'] // 调用搜狐接口获取设备IP
    }).then((response) => {
      if (response.result) {
        this.weChatParameter = response.result.wxPayReqData
        let url = process.env.API_WEB + process.env.IMG_BASE + '/?open_id=' + getUrlParams().open_id + '#' + this.$route.path // 之后需要跳转的页面
        window.location.href = response.result.wxPayReqData.mwebUrl + '&redirect_url=' + encodeURIComponent(url)
        }
      }
      this.disabledRecharge = false
    })
  } else {
    this.$toast.fail('请选择或输入充值金额')
  }
}
```

完美？NO！

安卓手机确实是没问题，支付完成后，自动回跳到app界面。但是苹果手机微信支付完成后，回调页面默认打开了safari 浏览器。（哭哭）

找了很久解决方案。最后！终于完成了，感谢天地。

解决方案：加一个中间页，用户触发点击事件后，再跳转回 app。

```js
doRecharge () {
  if (this.totalAmount || this.customMoney) {
    this.disabledRecharge = true
    this.$post('/wwt/pay/doRecharge', {
      accountNo: window.localStorage.accountNo,
      customerId: this.customerId,
      supplierId: window.localStorage.supplierId,
      totalAmount: this.totalAmount || this.customMoney,
      userName: window.localStorage.userName,
      ip: returnCitySN['cip'] // 调用搜狐接口获取设备IP
    }).then((response) => {
      if (response.result) {
        this.weChatParameter = response.result.wxPayReqData
        let url = process.env.API_WEB + process.env.IMG_BASE + '/?open_id=' + getUrlParams().open_id + '#' + this.$route.path // 之后需要跳转的页面
        if (this.versionJudge().ios) {
          let iosUrl = process.env.API_WEB + process.env.IMG_BASE + '/?open_id=' + getUrlParams().open_id + '#' + '/paySuccess' // 之后需要跳转的页面
          const iframe = document.createElement('iframe')
          iframe.style.display = 'none'
          iframe.setAttribute('src', response.result.wxPayReqData.mwebUrl + '&redirect_url=' + encodeURIComponent(iosUrl))
          iframe.setAttribute('sandbox', 'allow-top-navigation allow-scripts')
          document.body.appendChild(iframe)
        } else {
          window.location.href = response.result.wxPayReqData.mwebUrl + '&redirect_url=' + encodeURIComponent(url)
        }
      }
      this.disabledRecharge = false
    })
  } else {
    this.$toast.fail('请选择或输入充值金额')
  }
},
versionJudge () {
  var u = navigator.userAgent
  console.log(u)
  return {
    trident: u.indexOf('Trident') > -1, // IE内核
    presto: u.indexOf('Presto') > -1, // opera内核
    webKit: u.indexOf('AppleWebKit') > -1, // 苹果、谷歌内核
    gecko: u.indexOf('Gecko') > -1 && u.indexOf('KHTML') === -1, // 火狐内核
    mobile: !!u.match(/AppleWebKit.*Mobile.*/) || !!u.match(/AppleWebKit/), // 是否为移动终端
    ios: !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/), // ios终端
    android: u.indexOf('Android') > -1 || u.indexOf('Linux') > -1, // android终端或者uc浏览器
    iPhone: u.indexOf('iPhone') > -1 || u.indexOf('Mac') > -1, // 是否为iPhone或者QQHD浏览器
    iPad: u.indexOf('iPad') > -1, // 是否iPad
    isSafari: u.indexOf('Safari') !== -1 && u.indexOf('Chrome') === -1
  }
}
```

新增的中间页 `paySuccess.vue`：

```js
<template>
  <div class="pay-success">
    <img :src="imgBaseUrl + '/static/images/wxpay.png'" />
    <p>确认成功支付并返回蒙速办APP</p>
    <van-button type="primary" @click="goToApp">支付成功</van-button>
    <van-button type="primary" @click="goToApp">取消支付</van-button>
  </div>
</template>

<script>
export default {
  data () {
    return {}
  },
  methods: {
    goToApp () {
      if (this.versionJudge().isSafari) {
        window.location.href = 'mengsuban://'
      } else {
        this.$router.push({ name: 'RechargePayment' })
      }
    },
    versionJudge () {
      var u = navigator.userAgent
      return {
        trident: u.indexOf('Trident') > -1, // IE内核
        presto: u.indexOf('Presto') > -1, // opera内核
        webKit: u.indexOf('AppleWebKit') > -1, // 苹果、谷歌内核
        gecko: u.indexOf('Gecko') > -1 && u.indexOf('KHTML') === -1, // 火狐内核
        mobile: !!u.match(/AppleWebKit.*Mobile.*/) || !!u.match(/AppleWebKit/), // 是否为移动终端
        ios: !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/), // ios终端
        android: u.indexOf('Android') > -1 || u.indexOf('Linux') > -1, // android终端或者uc浏览器
        iPhone: u.indexOf('iPhone') > -1 || u.indexOf('Mac') > -1, // 是否为iPhone或者QQHD浏览器
        iPad: u.indexOf('iPad') > -1, // 是否iPad
        isSafari: u.indexOf('Safari') !== -1 && u.indexOf('Chrome') === -1
      }
    }
  },
  mounted () {
    if (this.versionJudge().isSafari) {
      window.location.href = 'mengsuban://'
    } else {
      this.$router.push({ name: 'RechargePayment' })
    }
  }
}
</script>

<style lang="less">
.pay-success {
  padding: 60px 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  img {
    height: 80px;
    margin-bottom: 20px;
  }
  p {
    margin-bottom: 20px;
  }
  button {
    width: 50%;
    border-radius: 5px;
    &:nth-of-type(1) {
      margin-top: 30px;
    }
    &:nth-of-type(2) {
      margin-top: 20px;
      background: rgba(214, 214, 214);
      border: rgba(214, 214, 214);
      color: rgba(168, 168, 168);
    }
  }
}
</style>
```
