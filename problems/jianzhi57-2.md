# 和为s的连续正数序列
剑指57-2 | [Link](https://leetcode-cn.com/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof/)

## 题目
输入一个正整数 target ，输出所有和为 target 的连续正整数序列（至少含有两个数）。

序列内的数字由小到大排列，不同序列按照首个数字从小到大排列。
```
示例 1：
输入：target = 9
输出：[[2,3,4],[4,5]]

示例 2：
输入：target = 15
输出：[[1,2,3,4,5],[4,5,6],[7,8]]

限制：
1 <= target <= 10^5
```

## 解答
用双指针/滑动窗口从最左边开始，根据和与目标值的比较，右移左边界或有边界，先找到最短的那个序列，找到后再往右扩充。

时间复杂度：O(N), 空间复杂度: O(1) 不算答案数组
```python
class Solution:
    def findContinuousSequence(self, target: int) -> List[List[int]]:
        l, r = 1, 2
        ssum = 3
        res = []
        while r <= target//2 + 1:
            if ssum < target:
                r += 1
                ssum += r
            elif ssum > target:
                ssum -= l
                l += 1
            else:
                res.append(list(range(l,r+1)))
                r += 1
                ssum += r
        return res
```