# 二叉搜索树的后序遍历序列
剑指33 | [Link](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/)

## 题目
输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历结果。如果是则返回 true，否则返回 false。假设输入的数组的任意两个数字都互不相同。
```
参考以下这颗二叉搜索树：
     5
    / \
   2   6
  / \
 1   3

示例 1：
输入: [1,6,3,2,5]
输出: false

示例 2：
输入: [1,3,2,6,5]
输出: true

限制：
数组长度 <= 1000
```

## 解答
后序遍历是（左，右，根），要保证二叉搜索树的性质的话需要把第一个值和所有后边的值比较。如果后序排列不好做的话，考虑先序排列的做法，左右子树的值和根比较。一次遍历就可以。而后 __序遍历倒序（根，右，左）__ 和先序类似，使得这个算法得以实现。
具体来说，用一个单调stack储存递增节点（就是一层一层root），每当遇到递减节点时，就通过出栈更新root。

时间复杂度：O(N), 空间复杂度: O(N)
```python
class Solution:
    def verifyPostorder(self, postorder: List[int]) -> bool:
    # 认为原来的树是root inf的左子树
        root, stack = float('inf'), []
        for i in range(len(postorder)-1, -1, -1):
            if postorder[i] > root: # 左子树都小于root
                return False
            while stack and postorder[i] < stack[-1]: # stack空的时候代表右半个树走完了
                root = stack.pop() # 更新root
            stack.append(postorder[i])
        return True
```