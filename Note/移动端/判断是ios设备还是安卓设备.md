<!--
 * @FileDescription: 
 * @Author: luyaj
 * @Date: 2020-09-23 17:48:52
 * @LastEditors: luyaj
 * @LastEditTime: 2020-09-23 17:50:12
-->
```js
function IsIOS() {
  if (/(iPhone|iPad|iPod|iOS)/i.test(navigator.userAgent)) {
    return true
  } else {
    return false
  }
}

function IsAndroid() {
  if (/(Android|Adr)/i.test(navigator.userAgent)) {
    return true
  } else {
    return false
  }
}
```