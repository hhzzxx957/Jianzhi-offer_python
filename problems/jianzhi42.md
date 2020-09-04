# 连续子数组的最大和
剑指41 | [Link](https://leetcode-cn.com/problems/lian-xu-zi-shu-zu-de-zui-da-he-lcof/)

## 题目
输入一个整型数组，数组中的一个或连续多个整数组成一个子数组。求所有子数组的和的最大值。

要求时间复杂度为O(n)。
```
示例1:
输入: nums = [-2,1,-3,4,-1,2,1,-5,4]
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。

限制：
1 <= arr.length <= 10^5
-100 <= arr[i] <= 100
```

## 解答
动态规划。我们可以直接遍历数组，得到当前值为结尾所能得到的子数组的最大和。每新加一个数，加到之前的结果里（如果之前的结果是负数，就扔掉）。

时间复杂度：O(N), 空间复杂度: O(1)
```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        for i in range(1, len(nums)):
            nums[i] += max(nums[i-1], 0)
        return max(nums)
```