# 从上到下打印二叉树 III
剑指32-3 | [Link](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/)

## 题目
请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推。
```
例如:
给定二叉树: [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
返回其层次遍历结果：
[
  [3],
  [20,9],
  [15,7]
]
 
限制：
节点总数 <= 1000
```

## 解答
在上一题的基础之上，再判断一下层数是奇还是偶。

时间复杂度：O(N), 空间复杂度: O(N)
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        if not root: return []
        res, queue = [], collections.deque()
        queue.append((0, root))
        while queue:
            level, node = queue.popleft()
            if level >= len(res): # new layer, add a list
                res.append([node.val]) 
            else:
                if level&1 == 1:
                    res[level].insert(0, node.val)
                else:
                    res[level].append(node.val)
            if node.left:
                queue.append((level+1, node.left))
            if node.right:
                queue.append((level+1,node.right))
        return res
```