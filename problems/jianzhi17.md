# 打印从1到最大的n位数
剑指17 | [Link](https://leetcode-cn.com/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/)

## 题目
输入数字 n，按顺序打印出从 1 到最大的 n 位十进制数。比如输入 3，则打印出 1、2、3 一直到最大的 3 位数 999。
```
示例 1:
输入: n = 1
输出: [1,2,3,4,5,6,7,8,9]

限制：
用返回一个整数列表来代替打印
n 为正整数
```

## 解答
此题考查大数越界的问题。对于Python由于语言特性没这个问题，我们可以写成
```python
class Solution:
    def printNumbers(self, n: int) -> List[int]:
        return list(range(1, 10**n))
```

如果要模拟避免大数越界，真的解决这个问题，我们可以用字符串表示数字。因为字符串没法直接加减，我们需要采用其他方法。我们可以看出，所要打印的结果是0到9的全排列。

时间复杂度：O(10<sup>N</sup>), 空间复杂度: O(N)

```python
class Solution:
    def printNumbers(self, n: int) -> List[int]:
        def dfs(ind):
            if ind == n:
                res.append(int(''.join(temp)))
                return
            for i in range(10):
                temp[ind] = chr(ord('0') + i)
                dfs(ind+1)

        temp = ['0']*n
        res = []
        dfs(0)
        return res[1:]
```
其实这个解法还是有点问题，我们用了int(''.join(temp))只是为了运行通过，依然有越界问题。同时这还避免了开头是0，如0007的情况。如果输出是字符串的list，我们应去掉高位的零。注意进位的情况。
```python
class Solution:
    def printNumbers(self, n: int) -> [int]:
        def dfs(ind):
            if ind == n:
                start = 0
                for char in temp:
                    if char == '0': start += 1
                    else: break
                s = ''.join(temp[start:]) # 剪掉前面的0
                if s: res.append(int(s)) # 第一个数都是0，去掉
                return
            for i in range(10):
                temp[ind] = chr(ord('0') + i)
                dfs(ind + 1)
        
        temp, res = ['0'] * n, []
        dfs(0)
        return res
```