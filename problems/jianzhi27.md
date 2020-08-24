# 二叉树的镜像
剑指27 | [Link](https://leetcode-cn.com/problems/er-cha-shu-de-jing-xiang-lcof/)

## 题目
请完成一个函数，输入一个二叉树，该函数输出它的镜像。
```
例如输入：

     4
   /   \
  2     7
 / \   / \
1   3 6   9
镜像输出：
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

```
示例：
输入：root = [4,2,7,1,3,6,9]
输出：[4,7,2,9,6,3,1]

限制：
0 <= 节点个数 <= 1000
```

## 解答
递归遍历(dfs)让每个节点的左子树和右子树调换。因为是先序遍历，所以由上至下翻转。

时间复杂度：O(N), 空间复杂度: O(N)
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def mirrorTree(self, root: TreeNode) -> TreeNode:
        if not root: return 
        root.left, root.right = root.right, root.left
        self.mirrorTree(root.left)
        self.mirrorTree(root.right)
        return root
```
---
## 解答2
既然是dfs，当然也可以用stack
```python
class Solution:
    def mirrorTree(self, root: TreeNode) -> TreeNode:
        if not root: return
        stack = [root]
        while stack:
            node = stack.pop()
            node.left, node.right = node.right, node.left
            if node.left: stack.append(node.left)
            if node.right: stack.append(node.right)
        return root
```