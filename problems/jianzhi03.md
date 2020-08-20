# 数组中重复的数字
剑指03 | [Link](https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/)

## 题目
找出数组中重复的数字。


在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

```
示例1：
输入：
[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3 

限制：
2 <= n <= 100000
```

## 方法1
用set来储存visited数字。python中set使用hash table实现的，查找是O(1)的复杂度。

时间复杂度：O(N), 空间复杂度: O(N)

```python
class Solution:
    def findRepeatNumber(self, nums: List[int]) -> int:
        numset = set()
        for num in nums:
            if num in numset:
                return num
            else:
                numset.add(num)
        return -1
```

## 方法2
如果需要实现原地操作，就要用到0~n-1的信息。我们可以看出索引和值是一对多的关系。如果利用交换，使得nums[i]=i，索引就可以起到dictionary的作用。

交换操作可以通过nums[nums[i]], nums[i]交换来实现，就是说使索引 nums[i] 处的值为 nums[i]。

时间复杂度：O(N), 空间复杂度: O(1)
```python
class Solution:
    def findRepeatNumber(self, nums: [int]) -> int:
        i = 0
        while i < len(nums):
            if nums[i] == i:
                i += 1
                continue
            if nums[nums[i]] == nums[i]: return nums[i]
            # 关键
            nums[nums[i]], nums[i] = nums[i], nums[nums[i]] 
        return -1
```



