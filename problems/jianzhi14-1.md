# 剪绳子
剑指14-1 | [Link](https://leetcode-cn.com/problems/jian-sheng-zi-lcof/)

## 题目
给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 k[0],k[1]...k[m-1] 。请问 k[0]*k[1]*...*k[m-1] 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。
```
示例 1：
输入: 2
输出: 1
解释: 2 = 1 + 1, 1 × 1 = 1

示例 2:
输入: 10
输出: 36
解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36

限制：
2 <= n <= 58
```

## 解答1
绳子按照 $x$ 长度等分为 $a$ 段，有$n=ax$,乘积为$x^a=x^{\frac{1}{x}n}$。于是，求乘积的极值,也就是求导为零可以写为

$$
\begin{aligned}
(x^a)' &= 0 \quad\quad \text{导数为0} \\\\
(x^{\frac{1}{x}})' &= 0 \quad\quad \text{n是常数} \\\\
({\frac{1}{x}}\ln x)'&= 0 \quad\quad \text{取log} \\\\
\frac{1}{x^2}-\frac{\ln x}{x^2} &= 0 \quad\quad \text{求导}\\\\
\ln x &= 1 \\\\
x & = e
\end{aligned}
$$

因为$x$必须取整数，我们取最接近的3，i.e. 把绳子尽可能切为长度为3的片段。
对于不能被3整除的情况，我们根据余数分类讨论。
余数为1时：取回一个3，变为2*2
余数为2时：直接乘2

时间复杂度：O(1), 空间复杂度: O(1)

```python
class Solution:
    def cuttingRope(self, n: int) -> int:
        if n <= 3: return n - 1
        a, b = n // 3, n % 3
        if b == 0: return pow(3, a)
        if b == 1: return pow(3, a - 1) * 4
        return pow(3, a) * 2
```
------
## 解答2
如果不喜欢数学解法，这里也提供一个动态规划的解法。关键点是转移方程
```python
dp[i] = max(dp[i], (i - j) * j, j * dp[i - j])
```
可以这么理解，右边dp[i]项的作用是保证不同剪法取最大的那个。(i-j)*i项是从j剪然后不往下剪了，j * dp[i - j]项是接着还往下剪。

时间复杂度：O(N<sup>2</sup>), 空间复杂度: O(N)
```python
class Solution:
    def cuttingRope(self, n: int) -> int:
        dp = [0 for _ in range(n + 1)] #0和1其实并没有用
        dp[2] = 1

        for i in range(3, n + 1):
            for j in range(i):
                dp[i] = max(dp[i], (i - j) * j, j * dp[i - j])
        return dp[n]
```