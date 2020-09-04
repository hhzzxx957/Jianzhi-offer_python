# 股票的最大利润
剑指63 | [Link](https://leetcode-cn.com/problems/gu-piao-de-zui-da-li-run-lcof/)

## 题目
假设把某股票的价格按照时间先后顺序存储在数组中，请问买卖该股票一次可能获得的最大利润是多少？
```
示例 1:
输入: [7,1,5,3,6,4]
输出: 5
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格。

示例 2:
输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
 
限制：
0 <= 数组长度 <= 10^5
```

## 解答
用动态规划。只要记录之前的最小值（成本），就能知道当前最大利润。

时间复杂度：O(N), 空间复杂度: O(1)
```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        minprice, profit = float('inf'), 0
        for price in prices:
            minprice = min(minprice, price)
            profit = max(profit, price - minprice)
        return profit
```