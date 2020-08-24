# 合并两个排序的链表
剑指25 | [Link](https://leetcode-cn.com/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof/)

## 题目
输入两个递增排序的链表，合并这两个链表并使新链表中的节点仍然是递增排序的。

```
示例：
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4

限制：
0 <= 链表长度 <= 1000
```

## 解答
新建一个伪头节点，然后从两个给定的链表里逐个往里链接值比较小的节点。注意一个链表走完的情况。

时间复杂度：O(M+N), 空间复杂度: O(1)
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        head = ListNode(0)
        curr = head
        while l1 and l2:
            if l1.val > l2.val:
                curr.next = l2
                l2 = l2.next
            else:
                curr.next = l1
                l1 = l1.next
            curr = curr.next
        if l1:
            curr.next = l1
        if l2:
            curr.next = l2
        return head.next
```