# 旋转数组的最小数字
剑指11 | [Link](https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/)

## 题目
把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个递增排序的数组的一个旋转，输出旋转数组的最小元素。例如，数组 [3,4,5,1,2] 为 [1,2,3,4,5] 的一个旋转，该数组的最小值为1。 

```
示例 1：
输入：[3,4,5,1,2]
输出：1

示例 2：
输入：[2,2,2,0,1]
输出：0
```

## 解答
查找问题第一反应就是二分法。不过因为数组旋转过，所以要仔细考虑判断条件。
我们考虑可能发生的情况。
1. 数组还是从小到大排的，对应左中右为，最小值在中间左边
2. 旋转过，最小值在中间左边
3. 旋转过，最小值在中间右面


|     |左 |中 |右 |最小值|
|-----|---|---|---|:---:|
|case1|小 |中 |大 |靠左  |
|case2|大 |小 |中 |靠左  |
|case3|中 |大 |小 |靠右  |
可以看出中间值比左边小的时候我们不知道最小值是不是在中间左面。所以我们采用**中间值和右边值比较**。

时间复杂度：log(N), 空间复杂度: O(1)
```python
class Solution:
    def minArray(self, nums: List[int]) -> int:
        if not nums:
            return None
        l, r = 0, len(nums)-1
        while l < r:
            mid=(l+r)//2 # or (l+r)>>1
            if(nums[mid]>nums[r]): # case3
                l=mid+1
            elif(nums[mid]<nums[r]): # case 1&2
                r=mid
            else: 
            # 中间值和右边相同，但不能确定最小值在哪边
            # 移去最右边一个依然可以保证有一个值在数组里
                r-=1
        return nums[l]
```