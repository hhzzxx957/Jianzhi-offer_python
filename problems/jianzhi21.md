# 调整数组顺序使奇数位于偶数前面
剑指21 | [Link](https://leetcode-cn.com/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/)

## 题目

```
示例：
输入：nums = [1,2,3,4]
输出：[1,3,2,4] 
注：[3,1,2,4] 也是正确的答案之一。

限制
1 <= nums.length <= 50000
1 <= nums[i] <= 10000
```

## 解答
用一个双向队列储存新加的数。奇数加到左边，偶数到右边。

时间复杂度：O(N), 空间复杂度: O(N)
```python
class Solution:
    def exchange(self, nums: List[int]) -> List[int]:
        if not nums:
            return nums
        resque = collections.deque()
        for num in nums:
            if num&1 == 1:
                resque.appendleft(num)
            else:
                resque.append(num)
        return list(resque)
```
----
## 解答2
通过两个指针交换的方法实现原地交换。
左指针遇到奇数就往右走，右指针遇到偶数就往左，从而保证交换的时候是奇偶互换到相同的地方。

时间复杂度：O(N), 空间复杂度: O(1)
```python
class Solution:
    def exchange(self, nums: List[int]) -> List[int]:
        left, right = 0, len(nums)-1
        while left < right:
            while left<right and nums[left]&1 == 1:
                left+=1
            while left<right and nums[right]&1 == 0:
                right-=1
            nums[left], nums[right] = nums[right], nums[left]
        return nums
```