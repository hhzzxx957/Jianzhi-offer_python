# 滑动窗口的最大值
剑指59-1 | [Link](https://leetcode-cn.com/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/)

## 题目
给定一个数组 nums 和滑动窗口的大小 k，请找出所有滑动窗口里的最大值。
```
示例:
输入: nums = [1,3,-1,-3,5,3,6,7], 和 k = 3
输出: [3,3,5,5,6,7] 
解释: 
  滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
 
限制：
你可以假设 k 总是有效的，在输入数组不为空的情况下，1 ≤ k ≤ 输入数组的大小。
```

## 解答
用一个双向队列作储存对应区域最大值（越往左越大），注意开始未形成窗口的情况。每次新加数的时候，就把比它小的最大值们pop掉。

时间复杂度：O(N), 空间复杂度: O(K)
```python
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        if not nums or k == 0: return []
        queue = collections.deque()
        for i in range(k): # 初始化，未形成窗口时
            while queue and nums[i] > queue[-1]:
                queue.pop()
            queue.append(nums[i])
        res = [queue[0]]
        for i in range(len(nums)-k): # i 是去掉的，i+k是加上的
            if nums[i] == queue[0]:
                queue.popleft()
            while queue and nums[i+k] > queue[-1]:
                queue.pop()
            queue.append(nums[i+k])
            res.append(queue[0])
        return res
```