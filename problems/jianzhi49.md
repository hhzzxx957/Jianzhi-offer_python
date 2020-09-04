# 丑数
剑指49 | [Link](https://leetcode-cn.com/problems/chou-shu-lcof/)

## 题目
我们把只包含质因子 2、3 和 5 的数称作丑数（Ugly Number）。求按从小到大的顺序的第 n 个丑数。
```
示例:
输入: n = 10
输出: 12
解释: 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 是前 10 个丑数。

限制:  
1 是丑数。
n 不超过1690。
```

## 解答
动态规划，我们从小到大依次生成丑数。因为丑数是以2，3，5为因子，所以每个新的丑数只可能是之前的乘2或3或5。我们需要找到下一个丑数是从哪个数乘起，然后乘那个数。

我们用三个数c2,c3,c5分别记录该乘2，3，5的那个数的索引。所以对应的候选就是
```
dp[c2]*2,dp[c3]*3,dp[c5]*5
```
，然后取最小的那个，同时更新对应的索引。

时间复杂度：O(N), 空间复杂度: O(N)
```python
class Solution:
    def nthUglyNumber(self, n: int) -> int:
        dp = [1]*n
        c2,c3,c5 = 0,0,0
        for i in range(1, n):
            candidates = [dp[c2]*2,dp[c3]*3,dp[c5]*5]
            dp[i] = min(candidates)
            if dp[i] == candidates[0]: c2 += 1
            if dp[i] == candidates[1]: c3 += 1
            if dp[i] == candidates[2]: c5 += 1
        return dp[-1]
```