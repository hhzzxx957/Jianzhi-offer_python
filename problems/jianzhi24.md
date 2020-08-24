# 反转链表
剑指24 | [Link](https://leetcode-cn.com/problems/fan-zhuan-lian-biao-lcof/)

## 题目
定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。
```
示例:
输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
 
限制：
0 <= 节点个数 <= 500
```

## 解答
用一个临时指针保存下一个的连接对象。

时间复杂度：O(N), 空间复杂度: O(1)
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        prev, curr = None, head
        while curr:
            temp = curr.next
            curr.next = prev
            prev, curr = curr, temp
        return prev
```