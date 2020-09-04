# 扑克牌中的顺子
剑指61 | [Link](https://leetcode-cn.com/problems/bu-ke-pai-zhong-de-shun-zi-lcof/)

## 题目
从扑克牌中随机抽5张牌，判断是不是一个顺子，即这5张牌是不是连续的。2～10为数字本身，A为1，J为11，Q为12，K为13，而大、小王为 0 ，可以看成任意数字。A 不能视为 14。
```
示例 1:
输入: [1,2,3,4,5]
输出: True

示例 2:
输入: [0,0,1,2,5]
输出: True

限制：
数组长度为 5 
数组的数取值为 [0, 13] .
```

## 解答
我们可以找最大最小值，只要maxnum - minnum >= 5，就return false。

时间复杂度：O(N), 空间复杂度: O(N)
```python
class Solution:
    def isStraight(self, nums: List[int]) -> bool:
        maxnum, minnum = float('-inf'), float('inf')
        visited = set()
        for num in nums:
            if num == 0: continue
            if num in visited: return False
            maxnum = max(maxnum, num)
            minnum = min(minnum, num)
            if maxnum - minnum >= 5: return False
            visited.add(num)
        return True
```