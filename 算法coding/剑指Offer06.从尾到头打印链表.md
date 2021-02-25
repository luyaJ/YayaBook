# 剑指Offer06.从尾到头打印链表

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

**示例 1：**

```
输入：head = [1,3,2]
输出：[2,3,1]
```

**限制：**

0 <= 链表长度 <= 10000

**JavaScript题解**：

执行用时：96 ms, 在所有 JavaScript 提交中击败了57.10%的用户
内存消耗：39.7 MB, 在所有 JavaScript 提交中击败了80.82%的用户

```JavaScript
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} head
 * @return {number[]}
 */
var reversePrint = function(head) {
    var arr = [];
    while(head !== null) {
        arr.push(head.val);
        head = head.next
    }
    arr.reverse();
    return arr;
};
```

**python题解**：

```python
class Solution:
    def reversePrint(self, head: ListNode) -> List[int]:
        stack = []
        while head:
            stack.append(head.val)
            head = head.next
        return stack[::-1]
```

[剑指offer 06 题目解析](https://leetcode-cn.com/leetbook/read/illustration-of-algorithm/5d8831/)