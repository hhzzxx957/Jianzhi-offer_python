# 数组中出现次数超过一半的数字
剑指39 | [Link](https://leetcode-cn.com/problems/shu-zu-zhong-chu-xian-ci-shu-chao-guo-yi-ban-de-shu-zi-lcof/)

## 题目
数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。
```
示例 1:
输入: [1, 2, 3, 2, 2, 2, 5, 4, 2]
输出: 2
 
限制：
1 <= 数组长度 <= 50000
```

## 解答
普通的思路就是用一个hashmap记录每个数的次数。时间空间都是O(N)。还有一种方法是投票法，就是“正负相消”的概念。因为众数大于一半，遇到两个数不一样就相消，留下的肯定是想找的结果。

时间复杂度：O(N), 空间复杂度: O(1)
```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        count, winner = 0, nums[0]
        for num in nums:
            if num == winner:
                count += 1
            else:
                count -= 1
                if count == 0:
                    winner = num
                    count += 1
        return winner
```