# n个骰子的点数
剑指60 | [Link](https://leetcode-cn.com/problems/nge-tou-zi-de-dian-shu-lcof/)

## 题目
把n个骰子扔在地上，所有骰子朝上一面的点数之和为s。输入n，打印出s的所有可能的值出现的概率。

你需要用一个浮点数数组返回答案，其中第 i 个元素代表这 n 个骰子所能掷出的点数集合中第 i 小的那个的概率。
```
示例 1:
输入: 1
输出: [0.16667,0.16667,0.16667,0.16667,0.16667,0.16667]

示例 2:
输入: 2
输出: [0.02778,0.05556,0.08333,0.11111,0.13889,0.16667,0.13889,0.11111,0.08333,0.05556,0.02778]

限制：
1 <= n <= 11
```

## 解答
动态规划，dp[i][j]代表仍i次骰子，得到和为j的可能情况的个数。
dp[i][j]可以通过dp[i-1][j-k] (k是1到7)来达到。于是关键就是
```
if j <= k: break
dp[i][j] += dp[i-1][j-k]
```

i的边界就是n，j的边界时6*i。最后结果是概率，除以6**n。

时间复杂度：O(N<sup>2</sup>), 空间复杂度: O(N<sup>2</sup>)
```python
class Solution:
    def twoSum(self, n: int) -> List[float]:
        dp = [[0 for _ in range(6*n+1)] for _ in range(n+1)]
        #dp[i][j], throw i times dice, result in sum of j

        for j in range(1,7):
            dp[1][j] = 1 
        
        for i in range(2, n+1):
            for j in range(i, 6*i+1):
                for k in range(1,7):
                    if j <= k: break
                    dp[i][j] += dp[i-1][j-k]
        res = []
        for j in range(n, 6*n+1):
            res.append(dp[n][j]/6**n)
        return res
```
# 解答2
因为下一层的状态只与上一层有关，所以我们可以优化空间。注意，为了避免在计算前覆盖上一层的结果，所以j要倒着写。还有提前终止条件改为j-k < i-1，因为少了一个的情况下，最小和为i-1。2d的没考虑这个是因为对应的值本来就是0。

时间复杂度：O(N<sup>2</sup>), 空间复杂度: O(N)
```python
class Solution:
    def twoSum(self, n: int) -> List[float]:
        dp = [0 for _ in range(6*n+1)]

        for j in range(1,7):
            dp[j] = 1 
        
        for i in range(2, n+1):
            for j in range(6*i, i-1,-1):
                dp[j]=0
                for k in range(1,7):
                    if j-k < i-1: break
                    dp[j] += dp[j-k]
        res = []
        for j in range(n, 6*n+1):
            res.append(dp[j]/6**n)
        return res
```