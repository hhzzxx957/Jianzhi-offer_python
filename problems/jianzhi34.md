# 二叉树中和为某一值的路径
剑指34 | [Link](https://leetcode-cn.com/problems/er-cha-shu-zhong-he-wei-mou-yi-zhi-de-lu-jing-lcof/)

## 题目
输入一棵二叉树和一个整数，打印出二叉树中节点值的和为输入整数的所有路径。从树的根节点开始往下一直到叶节点所经过的节点形成一条路径。
```
示例:
给定如下二叉树，以及目标和 sum = 22，

              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
返回:
[
   [5,4,11,2],
   [5,8,4,5]
]
 
限制：
节点总数 <= 10000
```

## 解答
典型的dfs问题。注意路径记录。其中path不能直接append，因为append会影响其他路径的path值。除了这种方法，也可以append到path的list之后，递归完当前路径之后再把这个值pop出去。

时间复杂度：O(N), 空间复杂度: O(N)
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def pathSum(self, root: TreeNode, target: int) -> List[List[int]]:
        def dfs(root, target, path, res):
            if not root: return
            target -= root.val
            if target == 0 and not root.left and not root.right:
                res.append(path + [root.val])

            dfs(root.left, target, path+[root.val], res)
            dfs(root.right, target, path+[root.val], res) 
        res = []
        dfs(root, target, [], res)
        return res
```