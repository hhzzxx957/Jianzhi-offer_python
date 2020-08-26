# 从上到下打印二叉树 II
剑指32-2 | [Link](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-ii-lcof/)

## 题目
从上到下打印出二叉树的每个节点，同一层的节点按照从左到右的顺序打印。
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
  [9,20],
  [15,7]
]
 
限制：
节点总数 <= 1000
```

## 解答
依然是BFS，再上一题的基础上多存储一个层数信息。就是说每次append不是一个值，是一对（层数，节点）。

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
                res[level].append(node.val)
            if node.left:
                queue.append((level+1, node.left))
            if node.right:
                queue.append((level+1,node.right))
        return res
```