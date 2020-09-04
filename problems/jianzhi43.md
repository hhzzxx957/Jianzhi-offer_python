# 1～n整数中1出现的次数
剑指43 | [Link](https://leetcode-cn.com/problems/1nzheng-shu-zhong-1chu-xian-de-ci-shu-lcof/)

## 题目
输入一个整数 n ，求1～n这n个整数的十进制表示中1出现的次数。

例如，输入12，1～12这些整数中包含1 的数字有1、10、11和12，1一共出现了5次。
```
示例 1：
输入：n = 12
输出：5

示例 2：
输入：n = 13
输出：6

限制：
1 <= n < 2^31
```

## 解答
一位一位来数1的个数。在找所在位1的个数与所在位的值(curr)，它之前的(high)和之后的值(low)都有关系。要考虑的关键就是能提供多少的digit。

1. curr = 0; 与low无关。high*digit
2. curr != 1; 与low无关。(high+1)*digit
3. curr = 1; 要考虑low。high*digit+low

时间复杂度：O(logN), 空间复杂度: O(1)
```python
class Solution:
    def countDigitOne(self, n: int) -> int:
        digit, res = 1, 0 # digit 所在位数（1，10，100……）
        high, curr, low = n // 10, n % 10, 0 # high/low means digits before/after curr
        while high != 0 or curr != 0:
            if curr == 0: res += high * digit # case 1
            elif curr == 1: res += high * digit + low + 1 # case 2
            else: res += (high + 1) * digit # case 3
            # update low, high, curr, digit
            low += curr * digit
            curr = high % 10
            high //= 10
            digit *= 10
        return res
```