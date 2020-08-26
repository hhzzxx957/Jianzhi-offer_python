# 对称的二叉树
剑指28 | [Link](https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof/)

## 题目
请实现一个函数，用来判断一棵二叉树是不是对称的。如果一棵二叉树和它的镜像一样，那么它是对称的。

```
例如，二叉树 [1,2,2,3,4,4,3] 是对称的。
    1
   / \
  2   2
 / \ / \
3  4 4  3
但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:
    1
   / \
  2   2
   \   \
   3    3
```

```
示例 1：
输入：root = [1,2,2,3,4,4,3]
输出：true

示例 2：
输入：root = [1,2,2,null,3,null,3]
输出：false
```

## 解答
迭代检查是不是每个
* 左节点的右子树和右节点的左子树 （l.right, r.left）
* 左节点的左子树和右节点的右子树 （l.left, r.right）

相同。
注意空节点的情况。

时间复杂度：O(N), 空间复杂度: O(N)
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        if not root: return True
        return self.checker(root.left, root.right)

    def checker(self, l, r):
        if not l and not r: return True
        if not l or not r: return False
        if l.val != r.val: return False
        return self.checker(l.right, r.left) and self.checker(l.left, r.right)
```