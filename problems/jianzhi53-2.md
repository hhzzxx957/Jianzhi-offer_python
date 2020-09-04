# 0～n-1中缺失的数字
剑指53-2 | [Link](https://leetcode-cn.com/problems/que-shi-de-shu-zi-lcof/)

## 题目
一个长度为n-1的递增排序数组中的所有数字都是唯一的，并且每个数字都在范围0～n-1之内。在范围0～n-1内的n个数字中有且只有一个数字不在该数组中，请找出这个数字。
```
示例 1:
输入: [0,1,3]
输出: 2

示例 2:
输入: [0,1,2,3,4,5,6,7,9]
输出: 8

限制：
1 <= 数组长度 <= 10000
```

## 解答
二分法。判断条件改为nums[mid] == mid。如果true证明缺的在右面，反之，在左面。

时间复杂度：O(logN), 空间复杂度: O(1)
```python
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        l, r = 0, len(nums)-1
        while l <= r:
            mid = (l+r)>>1
            if nums[mid] == mid:
                l = mid + 1 
            else:
                r = mid - 1
        return l
```