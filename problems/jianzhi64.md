# 求1+2+…+n
剑指64 | [Link](https://leetcode-cn.com/problems/qiu-12n-lcof/)

## 题目
求 1+2+...+n ，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。
```
示例 1：
输入: n = 3
输出: 6

示例 2：
输入: n = 9
输出: 45

限制：
1 <= n <= 10000
```

## 解答
如果不用if如何终止递归。这里用到一个东西叫做逻辑运算符的短路效应。就是and之前如果是false的话后面就不执行了。同理，如果or之前是true，后面也不执行了。

时间复杂度：O(N), 空间复杂度: O(1)
```python
class Solution:
    def __init__(self):
        self.res = 0
    def sumNums(self, n: int) -> int:
        n > 1 and self.sumNums(n-1)
        self.res += n
        return self.res    
```