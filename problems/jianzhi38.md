# 字符串的排列
剑指38 | [Link](https://leetcode-cn.com/problems/zi-fu-chuan-de-pai-lie-lcof/)

## 题目
输入一个字符串，打印出该字符串中字符的所有排列。
你可以以任意顺序返回这个字符串数组，但里面不能有重复元素。
```
示例:
输入：s = "abc"
输出：["abc","acb","bac","bca","cab","cba"]

限制：
1 <= s 的长度 <= 8
```

## 解答
回溯法遍历。注意不要直接改lists和path的值。先对s排序，以避免重复结果。

时间复杂度：O(N!), 空间复杂度: O(N<sup>2</sup>)
```python
class Solution:
    def permutation(self, s: str) -> List[str]:
        def recur(lists, path, res):
            if not lists:
                res.append(''.join(path))
                return
            for i, char in enumerate(lists):
                if i>0 and lists[i]==lists[i-1]:
                    continue
                recur(lists[:i]+lists[i+1:], path+[char], res)
        
        lists = list(sorted(s))
        res = []

        recur(lists, [], res)
        return res
```