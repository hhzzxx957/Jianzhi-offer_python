# 在排序数组中查找数字
剑指53-1 | [Link](https://leetcode-cn.com/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/)

## 题目
统计一个数字在排序数组中出现的次数。

```
示例 1:
输入: nums = [5,7,7,8,8,10], target = 8
输出: 2

示例 2:
输入: nums = [5,7,7,8,8,10], target = 6
输出: 0
 
限制：
0 <= 数组长度 <= 50000
```

## 解答
找到最左和最右边的这个数。分别用二分法跑两边，区别是判断的时候用<还是<=。

时间复杂度：O(logN), 空间复杂度: O(1)
```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        l, r = 0, len(nums)-1
        while l <= r:
            mid = (l+r)>>1
            if nums[mid] <= target:
                l = mid + 1
            else:
                r = mid - 1
        right = r

        l, r = 0, len(nums)-1
        while l <= r:
            mid = (l+r)>>1
            if nums[mid] < target:
                l = mid + 1
            else:
                r = mid - 1
        left = l

        return right - left + 1
```