# 数组中的逆序对
剑指51 | [Link](https://leetcode-cn.com/problems/shu-zu-zhong-de-ni-xu-dui-lcof/)

## 题目
在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组，求出这个数组中的逆序对的总数。在合并的时候，如果时候一个后一个数组的数小，我们就可以组成mid-i+1个逆序对。i是前一个数组的索引。

```
示例 1:
输入: [7,5,6,4]
输出: 5
 

限制：
0 <= 数组长度 <= 50000
```

## 解答
用分治的方法来提高效率，在归并的时候计算逆序对。

时间复杂度：O(NlogN), 空间复杂度: O(N)
```python
class Solution:
    def reversePairs(self, nums: List[int]) -> int:
        def merge(nums, start, end, mid, temp):
            i, j = start, mid+1
            while i <= mid and j <= end:
                if nums[i] <= nums[j]:
                    temp.append(nums[i])
                    i += 1
                else: # 逆序情况
                    temp.append(nums[j])
                    self.count += mid-i+1  # 关键
                    j += 1
            if i <= mid: # 补完剩下的
                temp.extend(nums[i:mid+1])
            if j <= end:
                temp.extend(nums[j:end+1])
            nums[start:end+1] = temp # 把排好的数组放回去
            temp.clear()

        def mergesort(nums, start, end, temp):
            if start >= end: return
            mid = (start+end)>>1
            mergesort(nums, start, mid, temp) # 用同一个temp节省空间
            mergesort(nums, mid+1, end, temp)
            merge(nums, start, end, mid, temp)

        self.count = 0
        mergesort(nums, 0, len(nums)-1, [])

        return self.count
```