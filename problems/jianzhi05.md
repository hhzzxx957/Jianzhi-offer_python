# 替换空格
剑指05 | [Link](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/)

## 题目
请实现一个函数，把字符串 s 中的每个空格替换成"%20"。
```
示例:
输入：s = "We are happy."
输出："We%20are%20happy."

限制：
0 <= s 的长度 <= 10000
```

## 解答
...
Python中string是不可变immutable的。
用一个list来存储结果。
时间复杂度：O(N), 空间复杂度: O(N)
```python
class Solution:
    def replaceSpace(self, s: str) -> str:
        res = []
        for char in s:
            if char == ' ':
                res.append('%20')
            else:
                res.append(char)
        return ''.join(res)
```