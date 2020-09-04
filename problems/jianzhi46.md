# 把数字翻译成字符串
剑指46 | [Link](https://leetcode-cn.com/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/)

## 题目
给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。
```
示例 1:
输入: 12258
输出: 5
解释: 12258有5种不同的翻译，分别是"bccfi", "bwfi", "bczi", "mcfi"和"mzi"

提示：
0 <= num < 2^31
```

## 解答
动态规划。dp的值就是翻译方法的个数。只要当前翻译的字符和上一个在'10'到'25'之间，就把上一个状态个数也加到下一个状态（对应两种翻译方法）。

时间复杂度：O(N), 空间复杂度: O(1)
```python
class Solution:
    def translateNum(self, num: int) -> int:
        s = str(num)
        prev, curr = 1, 1
        for i in range(2, len(s)+1):
            if '10' <= s[i-2:i] <='25'：nxt = prev+curr
            else: nxt = curr
            prev, curr = curr, nxt
        return curr
```