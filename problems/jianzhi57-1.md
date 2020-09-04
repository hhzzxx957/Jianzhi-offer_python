# 和为s的两个数字
剑指57-1 | [Link](https://leetcode-cn.com/problems/he-wei-sde-liang-ge-shu-zi-lcof/)

## 题目
输入一个递增排序的数组和一个数字s，在数组中查找两个数，使得它们的和正好是s。如果有多对数字的和等于s，则输出任意一对即可。
```
示例 1：
输入：nums = [2,7,11,15], target = 9
输出：[2,7] 或者 [7,2]

示例 2：
输入：nums = [10,26,30,31,47,60], target = 40
输出：[10,30] 或者 [30,10]

限制：
1 <= nums.length <= 10^5
1 <= nums[i] <= 10^6
```

## 解答
因为是递增排序的数组，我们可以用双指针来处理。通过两个指针对应值的和与目标值比较来逼近。

时间复杂度：O(N), 空间复杂度: O(1)
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        lp, rp = 0, len(nums)-1
        while lp < rp:
            if nums[lp] + nums[rp] == target:
                return (nums[lp], nums[rp])
            if nums[lp] + nums[rp] > target:
                rp -= 1
            else:
                lp += 1
```