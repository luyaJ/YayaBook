判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

**示例 1:**
```js
输入: 121
输出: true
```

**示例 2:**
```js
输入: -121
输出: false
解释: 从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。
```

**示例 3:**
```js
输入: 10
输出: false
解释: 从右向左读, 为 01 。因此它不是一个回文数。
```

字符串解法：
```js
/**
 * @param {number} x
 * @return {boolean}
 */
var isPalindrome = function(x) {
  var x_string = x.toString(); // 转换成字符串
  return x_string.split('').reverse().join('') === x_string;
};
```