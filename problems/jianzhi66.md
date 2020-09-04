# 构建乘积数组
剑指66 | [Link](https://leetcode-cn.com/problems/gou-jian-cheng-ji-shu-zu-lcof/)

## 题目
给定一个数组 A[0,1,…,n-1]，请构建一个数组 B[0,1,…,n-1]，其中 B 中的元素 B[i]=A[0]×A[1]×…×A[i-1]×A[i+1]×…×A[n-1]。不能使用除法。
```
示例:
输入: [1,2,3,4,5]
输出: [120,60,40,30,24]

限制：
所有元素乘积之和不会溢出 32 位整数
a.length <= 100000
```

## 解答
dp题。关键在于中间缺了一个不连续了。解决办法就是用两个循环分别从大到小和从小到大构建两个连续的连乘。

时间复杂度：O(N), 空间复杂度: O(N)
```python
class Solution:
    def constructArr(self, a: List[int]) -> List[int]:
        b = [1]*len(a)
        for i in range(1, len(a)):
            b[i] = b[i-1] * a[i-1]
        value = 1
        for i in range(len(a)-2, -1, -1):
            value *= a[i+1]
            b[i] *= value
        return b
```