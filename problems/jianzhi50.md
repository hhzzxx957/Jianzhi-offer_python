# 第一个只出现一次的字符
剑指50 | [Link](https://leetcode-cn.com/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/)

## 题目
在字符串 s 中找出第一个只出现一次的字符。如果没有，返回一个单空格。 s 只包含小写字母。
```
示例:
s = "abaccdeff"
返回 "b"

s = "" 
返回 " "

限制：
0 <= s 的长度 <= 50000
```

## 解答
用hashmap完成查找。

时间复杂度：O(N), 空间复杂度: O(N)
```python
class Solution:
    def firstUniqChar(self, s: str) -> str:
        dic = {}
        for char in s:
            if char in dic:
                dic[char] += 1
            else:
                dic[char] = 1
        for char in dic:
            if dic[char] == 1:
                return char
        return " "
```