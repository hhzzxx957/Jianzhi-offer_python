# 数组中数字出现的次数
剑指56-1 | [Link](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-lcof/)

## 题目
一个整型数组 nums 里除两个数字之外，其他数字都出现了两次。请写程序找出这两个只出现一次的数字。要求时间复杂度是O(n)，空间复杂度是O(1)。
```
示例 1：
输入：nums = [4,1,4,6]
输出：[1,6] 或 [6,1]

示例 2：
输入：nums = [1,2,10,4,1,4,3,3]
输出：[2,10] 或 [10,2]

限制：
2 <= nums.length <= 10000
```

## 解答
因为要求空间复杂度是O(1)，所以不能用hashmap来做。可以用位运算来做。因为相同的数取异或的话就消了，于是可以找到单个的数字，接下来的问题是怎么把它们分开。

我们取一个mask，记录是1的最低位（在这一位这两个数不同，且肯定存在这样一位，否则这两个数就一样了）。最后再通过两个循环的异或得到单个的两个数（通过与mask的与运算判断）。

时间复杂度：O(N), 空间复杂度: O(1)
```python
class Solution:
    def singleNumbers(self, nums: List[int]) -> List[int]:
        n1, n2 = 0, 0
        xor = 0
        for num in nums:
            xor ^= num
        mask = 1
        while xor & mask == 0:
            mask <<= 1
        
        for num in nums:
            if num & mask == 0:
                n1 ^= num
            else:
                n2 ^= num
        return [n1, n2]
```