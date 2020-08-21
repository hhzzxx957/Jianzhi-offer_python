# 青蛙跳台阶问题
剑指10-2 | [Link](https://leetcode-cn.com/problems/qing-wa-tiao-tai-jie-wen-ti-lcof/)

## 题目
一只青蛙一次可以跳上1级台阶，也可以跳上2级台阶。求该青蛙跳上一个 n 级的台阶总共有多少种跳法。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

```
示例 1：
输入：n = 2
输出：2

示例 2：
输入：n = 7
输出：21

示例 3：
输入：n = 0
输出：1

限制：
0 <= n <= 100
```

## 解答
另一道经典dp题。思路和斐波那契数列一样，只不过更改了初始值。

时间复杂度：O(N), 空间复杂度: O(1)
```python
class Solution:
    def numWays(self, n: int) -> int:
        prev_count, curr_count = 1, 1
        for _ in range(n-1):
            prev_count, curr_count = curr_count, prev_count+curr_count
        return curr_count%(10**9+7)
```