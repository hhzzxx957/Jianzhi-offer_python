# 二叉搜索树与双向链表
剑指36 | [Link](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-yu-shuang-xiang-lian-biao-lcof/)

## 题目
输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的循环双向链表。要求不能创建任何新的节点，只能调整树中节点指针的指向。

以下面的二叉搜索树为例：

![alt text](https://assets.leetcode.com/uploads/2018/10/12/bstdlloriginalbst.png "Binary Tree")

我们希望将这个二叉搜索树转化为双向循环链表。链表中的每个节点都有一个前驱和后继指针。对于双向循环链表，第一个节点的前驱是最后一个节点，最后一个节点的后继是第一个节点。

下图展示了上面的二叉搜索树转化成的链表。“head” 表示指向链表中有最小元素的节点。

![alt text](https://assets.leetcode.com/uploads/2018/10/12/bstdllreturndll.png "Linked list")

特别地，我们希望可以就地完成转换操作。当转化完成以后，树中节点的左指针需要指向前驱，树中节点的右指针需要指向后继。还需要返回链表中的第一个节点的指针。

## 解答
dfs中序（左，根，右）遍历整棵树。用两个变量记录当前节点和前一个节点。然后连接在一起。
```
prev.right = curr
curr.left = prev
```
注意最后一个节点链接回head。

时间复杂度：O(N), 空间复杂度: O(N)
```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
"""
class Solution:
    def treeToDoublyList(self, root: 'Node') -> 'Node':
        def dfs(curr):
            if not curr: return None
            dfs(curr.left)

            if self.prev: # link curr and pre nodes
                self.prev.right = curr
                curr.left = self.prev
            else:
                self.head = curr # left most node (smallest)
            self.prev = curr

            dfs(curr.right)
        if not root: return root
        self.prev = None # use self to extract last node
        dfs(root)
        # connect lost node to head node
        self.head.left, self.prev.right = self.prev, self.head
        
        return self.head
```