# 数组中数字出现的次数 II
剑指56-2 | [Link](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-ii-lcof/)

## 题目
在一个数组 nums 中除一个数字只出现一次之外，其他数字都出现了三次。请找出那个只出现一次的数字。
```
示例 1：
输入：nums = [3,4,3,3]
输出：4

示例 2：
输入：nums = [9,1,7,9,7,9,7]
输出：1

限制：
1 <= nums.length <= 10000
1 <= nums[i] < 2^31
```

## 解答
同样用位运算处理这道题。关键点是对每一位计数，然后对3取余，这个方法同样适用于n个数。

时间复杂度：O(N), 空间复杂度: O(1)
```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        res, bit = 0, 1
        for i in range(32):
            count = 0
            for num in nums:
                if num & bit != 0: count += 1
            if count%3 != 0:
                res |= bit
            bit <<= 1
        return res if res <= 2**31 else res - 2**32
```