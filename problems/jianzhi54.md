# 二叉搜索树的第k大节点
剑指54 | [Link](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/)

## 题目
给定一棵二叉搜索树，请找出其中第k大的节点。
```
示例 1:
输入: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
输出: 4

示例 2:
输入: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
输出: 4

限制：
1 ≤ k ≤ 二叉搜索树元素个数
```

## 解答
dfs中序遍历。用两个类变量记录k和第k个的值。

时间复杂度：O(N), 空间复杂度: O(N)
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def kthLargest(self, root: TreeNode, k: int) -> int:
        def dfs(root):
            if not root: return
            dfs(root.right)
            self.k -= 1
            if self.k == 0: 
                self.res = root.val
                return
            dfs(root.left)

        self.k = k
        dfs(root)
        return self.res
```