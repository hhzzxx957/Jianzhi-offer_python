# 序列化二叉树
剑指37 | [Link](https://leetcode-cn.com/problems/xu-lie-hua-er-cha-shu-lcof/)

## 题目
请实现两个函数，分别用来序列化和反序列化二叉树。
```
示例: 
你可以将以下二叉树：

    1
   / \
  2   3
     / \
    4   5

序列化为 "[1,2,3,null,null,4,5]"
```

## 解答
BST遍历，用队列，注意输出格式。deserialize用相似的方法，特殊处理'null'。

时间复杂度：O(N), 空间复杂度: O(N)
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Codec:

    def serialize(self, root):
        """Encodes a tree to a single string.
        
        :type root: TreeNode
        :rtype: str
        """
        if not root: return '[]'
        queue = collections.deque()
        queue.append(root)
        res = []
        while queue:
            root = queue.popleft()
            if root:
                queue.append(root.left)
                queue.append(root.right)
                res.append(str(root.val))
            else:
                res.append('null')
        return '['+','.join(res)+']'
        

    def deserialize(self, data):
        """Decodes your encoded data to tree.
        
        :type data: str
        :rtype: TreeNode
        """
        if data == '[]': return None

        values = collections.deque(data[1:-1].split(','))
        root = TreeNode(int(values.popleft()))

        queue = collections.deque()
        queue.append(root)

        while queue:
            node = queue.popleft()
            left_value = values.popleft()
            if left_value != 'null':
                node.left = TreeNode(int(left_value))
                queue.append(node.left)

            right_value = values.popleft()
            if right_value != 'null':
                node.right = TreeNode(int(right_value))
                queue.append(node.right)

        return root

        

# Your Codec object will be instantiated and called as such:
# codec = Codec()
# codec.deserialize(codec.serialize(root))
```