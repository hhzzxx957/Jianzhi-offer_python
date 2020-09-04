# 不用加减乘除做加法
剑指65 | [Link](https://leetcode-cn.com/problems/bu-yong-jia-jian-cheng-chu-zuo-jia-fa-lcof/)

## 题目
写一个函数，求两个整数之和，要求在函数体内不得使用 “+”、“-”、“*”、“/” 四则运算符号。
```
示例:
输入: a = 1, b = 1
输出: 2

提示：
a, b 均可能是负数或 0
结果不会溢出 32 位整数
```

## 解答
位运算bit manipulation。对于没有进位的时候，所在位相加和异或^相同。进位结果和与&相同。所以思路就是先算非进位和a ^ b，再补上进位(a & b) << 1。

0xffffffff的作用就是保证32位以内。0x7fffffff是最大的正数的补码。~(a ^ x) 是将 32 位以上的位取反，1 至 32 位不变。

时间复杂度：O(1), 空间复杂度: O(1)
```python
class Solution:
    def add(self, a: int, b: int) -> int:
        x = 0xffffffff
        a, b = a & x, b & x
        while b:
            a, b = a ^ b, (a & b) << 1 & x
        return a if a <= 0x7fffffff else ~(a ^ x)
```