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