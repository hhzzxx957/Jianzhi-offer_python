# 二叉树的深度
剑指55-1 | [Link](https://leetcode-cn.com/problems/er-cha-shu-de-shen-du-lcof/)

## 题目
输入一棵二叉树的根节点，求该树的深度。从根节点到叶节点依次经过的节点（含根、叶节点）形成树的一条路径，最长路径的长度为树的深度。
```
例如：
给定二叉树 [3,9,20,null,null,15,7]，
    3
   / \
  9  20
    /  \
   15   7
返回它的最大深度 3 。

限制：
节点总数 <= 10000
```

## 解答
dfs遍历，用类变量记录最深的深度。

时间复杂度：O(N), 空间复杂度: O(N)
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def maxDepth(self, root: TreeNode) -> int:
        def dfs(node,layer):
            if not node: return
            self.res = max(self.res, layer)
            dfs(node.left, layer+1)
            dfs(node.right, layer+1)
        self.res = 0
        dfs(root, 1)
        return self.res
```