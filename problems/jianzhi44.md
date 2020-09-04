# 数字序列中某一位的数字
剑指44 | [Link](https://leetcode-cn.com/problems/shu-zi-xu-lie-zhong-mou-yi-wei-de-shu-zi-lcof/)

## 题目
数字以0123456789101112131415…的格式序列化到一个字符序列中。在这个序列中，第5位（从下标0开始计数）是5，第13位是1，第19位是4，等等。

请写一个函数，求任意第n位对应的数字。
```
示例 1：
输入：n = 3
输出：3

示例 2：
输入：n = 11
输出：0

限制：
0 <= n < 2^31
```

## 解答
一位一位的减数。个位9个，十位2*90个。。。

时间复杂度：..., 空间复杂度: ...
```python
class Solution:
    def findNthDigit(self, n: int) -> int:
        digit, count = 1, 9
        while n > count:
            n -= count
            digit += 1
            count = count*10*digit//(digit-1)
            # count = 9*digit*10**(digit-1) # 另一种写法
        # 找到对应的数    
        num = 10**(digit-1) + (n-1)//digit
        # 用字符串索引
        res = str(num)[(n-1)%digit]
        return int(res)
```