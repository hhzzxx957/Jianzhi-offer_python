# 从尾到头打印链表
剑指06 | [Link](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

## 题目
输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

```
示例:
输入：head = [1,3,2]
输出：[2,3,1]

限制：
0 <= 链表长度 <= 10000
```

## 解答
先入后出 的需求可以借助**栈**来实现。

时间复杂度：O(N), 空间复杂度: O(N)
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def reversePrint(self, head: ListNode) -> List[int]:
        stack = []
        while head:
            stack.append(head.val)
            head = head.next
        return stack[::-1]
```