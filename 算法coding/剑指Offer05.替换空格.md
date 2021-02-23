# 剑指Offer 05.替换空格

请实现一个函数，把字符串 `s` 中的每个空格替换成"%20"。

**示例1**：

```bash
输入：s = "We are happy."
输出："We%20are%20happy."
```

限制：0 <= s 的长度 <= 10000

**JavaScript 题解**：

```JavaScript
/**
 * @param {string} s
 * @return {string}
 */
var replaceSpace = function(s) {
    s = s.split('')
    for(let i = 0; i < s.length; i++) {
        if (s[i] === ' ') {
            s[i] = '%20'
        }
    }
    return s.join('')
};
```

**Python 题解**：

```python
class Solution:
    def replaceSpace(self, s: str) -> str:
        res = []
        for c in s:
            if c == ' ': res.append('%20')
            else: res.append(c)
        return ''.join(res)
```

[剑指offer 05 题目解析](https://leetcode-cn.com/leetbook/read/illustration-of-algorithm/50c26h/)