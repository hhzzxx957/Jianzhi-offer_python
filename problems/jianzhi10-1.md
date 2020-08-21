# 斐波那契数列
剑指10-I | [Link](https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof/)

## 题目
写一个函数，输入 n ，求斐波那契（Fibonacci）数列的第 n 项。斐波那契数列的定义如下：
```
F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), 其中 N > 1.
斐波那契数列由 0 和 1 开始，之后的斐波那契数就是由之前的两数相加而得出。
```
答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。


```
示例1:
输入：n = 2
输出：1

示例2:
输入：n = 5
输出：5

限制：
0 <= n <= 100
```

## 解答
经典dynamic programming(dp)题。
动态规划题从以下几方面入手：
|状态定义|转移方程         |初始状态  |返回值|
|:-----:|:---------------:|:-------:|:-----:|
|第i个数，dp[i]|f(i+1)=f(i)+f(i−1)|dp[0],dp[1]|dp[n]|

优化空间可以就用最近两个数。

时间复杂度：O(N), 空间复杂度: O(1)
```python
class Solution:
    def fib(self, n: int) -> int:
        if n == 0: return 0

        pre_num, curr_num = 0, 1

        for _ in range(n-1):
            pre_num, curr_num = curr_num, pre_num + curr_num

        return curr_num%(10**9+7)
```
-----
## 解答2
这里贴一个没有空间优化过的动态规划。

时间复杂度：O(N), 空间复杂度: O(N)
```python
class Solution:
    def fib(self, n: int) -> int:
        if n==0: return 0
        dp = [0,1]
        for _ in range(n-1):
            dp.append(dp[-1] + dp[-2])
        return dp[-1]%1000000007
```