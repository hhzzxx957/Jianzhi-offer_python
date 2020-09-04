# 平衡二叉树
剑指55-2 | [Link](https://leetcode-cn.com/problems/ping-heng-er-cha-shu-lcof/)

## 题目

```
示例 1:
给定二叉树 [3,9,20,null,null,15,7]
    3
   / \
  9  20
    /  \
   15   7
返回 true 。

示例 2:
给定二叉树 [1,2,2,3,3,null,null,4,4]
       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
返回 false 。

限制：
1 <= 树的结点个数 <= 10000
```

## 解答
dfs遍历。判断条件是左右深度差小于等于1。

时间复杂度：O(N), 空间复杂度: O(N)
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isBalanced(self, root: TreeNode) -> bool:
        def depth(node):
            if not node: return 0
            left = depth(node.left)
            right = depth(node.right)
            if left != -1 and right != -1 and abs(left - right) <= 1:
                return max(left, right) + 1
            else:
                return -1 # -1代表不平衡

        return depth(root) != -1
```