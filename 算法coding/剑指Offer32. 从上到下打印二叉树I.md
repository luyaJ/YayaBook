# 剑指Offer32. 从上到下打印二叉树I

从上到下打印出二叉树的每个节点，同一层的节点按照从左到右的顺序打印。

例如: 给定二叉树  `[3,9,20,null,null,15,7]`

```bash
       3
      / \
     9  20
        / \
       15   7
```

返回：`[3,9,20,15,7]`

**JavaScript题解**：

层序遍历需要使用一个队列来存储有用的节点，思路：

* 将 root 放入队列
* 取出队首元素，将 val 放入返回的数组中
* 检查队首元素的子节点，若不为空，则将子节点放入队列
* 检查队列是否为空，为空，结束并返回数组；不为空，继续从第二步执行

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number[]}
 */
var levelOrder = function(root) {
    if (!root) return [];

    let result = [], queue = [root];
    while (queue.length) {
        let node = queue.shift();
        result.push(node.val);

        node.left && queue.push(node.left);
        node.right && queue.push(node.right);
    }
    return result;
};
```

原题链接：https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof