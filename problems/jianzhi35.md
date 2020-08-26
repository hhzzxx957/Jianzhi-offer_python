# 复杂链表的复制
剑指35 | [Link](https://leetcode-cn.com/problems/fu-za-lian-biao-de-fu-zhi-lcof/)

## 题目
请实现 copyRandomList 函数，复制一个复杂链表。在复杂链表中，每个节点除了有一个 next 指针指向下一个节点，还有一个 random 指针指向链表中的任意节点或者 null。
```
示例 1：
输入：head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
输出：[[7,null],[13,0],[11,4],[10,2],[1,0]]

示例 2：
输入：head = [[1,1],[2,1]]
输出：[[1,1],[2,1]]

示例 3：
输入：head = [[3,null],[3,0],[3,null]]
输出：[[3,null],[3,0],[3,null]]

示例 4：
输入：head = []
输出：[]
解释：给定的链表为空（空指针），因此返回 null。

限制：
-10000 <= Node.val <= 10000
Node.random 为空（null）或指向链表中的节点。
节点数目不超过 1000 。
```

## 解答
这题的目的是实现链表的deep copy。既然要整个复制，就要遍历，用dfs。为了避免重复访问，用一个dictionary记录访问过的节点。

时间复杂度：O(N), 空间复杂度: O(N)
```python
"""
# Definition for a Node.
class Node:
    def __init__(self, x: int, next: 'Node' = None, random: 'Node' = None):
        self.val = int(x)
        self.next = next
        self.random = random
"""
class Solution:
    def copyRandomList(self, head: 'Node') -> 'Node':
        def dfs(head):
            if head in visiteddic:
                return visiteddic[head] # avoid infinite loop; don't create new node
            if not head: return None

            copy = Node(head.val, None, None) # create new node
            visiteddic[head] = copy
            copy.next = dfs(head.next)
            copy.random = dfs(head.random)
            
            return copy
        visiteddic = {}
        return dfs(head)
```