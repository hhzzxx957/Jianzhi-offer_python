# 把数组排成最小的数
剑指45 | [Link](https://leetcode-cn.com/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/)

## 题目
输入一个非负整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。
```
示例 1:
输入: [10,2]
输出: "102"

示例 2:
输入: [3,30,34,5,9]
输出: "3033459"

限制：
0 < nums.length <= 100

说明:
输出结果可能非常大，所以你需要返回一个字符串而不是整数
拼接起来的数字可能会有前导 0，最后结果不需要去掉前导 0
```

## 解答
这题可以看成是一种自定义的排序，而规则是
```
如果 x+y>y+x 则 x>y； x,y是字符串
```
我们可以用快排，只不过判断条件改一下。

时间复杂度：O(NlogN), 空间复杂度: O(N)
```python
class Solution:
    def minNumber(self, nums: List[int]) -> str:        
        arr = [str(i) for i in nums]
        self.quick_sort(arr, 0, len(nums)-1)
        return ''.join(arr)

    def quick_sort(self, arr, low, high):
        if low >= high: return
        pivot_index = self.partition(arr, low, high)

        self.quick_sort(arr, low, pivot_index - 1)
        self.quick_sort(arr, pivot_index + 1, high)

    def partition(self, arr, l, r):
        high = r
        pivot = arr[r]
        while l < r:
            while l < r and arr[l]+pivot < pivot+arr[l]: l += 1 # 改比较大小的判断条件
            while l < r and arr[r]+pivot >= pivot+arr[r]: r -= 1
            if l < r:
                arr[l], arr[r] = arr[r], arr[l]
        arr[r], arr[high] = arr[high], arr[r]
        return r
```