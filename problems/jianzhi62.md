# 圆圈中最后剩下的数字
剑指62 | [Link](https://leetcode-cn.com/problems/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-lcof/)

## 题目
0,1,,n-1这n个数字排成一个圆圈，从数字0开始，每次从这个圆圈里删除第m个数字。求出这个圆圈里剩下的最后一个数字。

例如，0、1、2、3、4这5个数字组成一个圆圈，从数字0开始每次删除第3个数字，则删除的前4个数字依次是2、0、4、1，因此最后剩下的数字是3。
```
示例 1：
输入: n = 5, m = 3
输出: 3

示例 2：
输入: n = 10, m = 17
输出: 2

限制：
1 <= n <= 10^5
1 <= m <= 10^6
```

## 解答
解约瑟夫环的问题。先看模拟法。

时间复杂度：O(MN), 空间复杂度: O(N)
```python
class Solution:
    def lastRemaining(self, n: int, m: int) -> int:
        listn = list(range(n))
        i = 0
        while len(listn)>1:
            i = (i+m-1) % len(listn)
            listn.pop(i)
        return listn[0]
```

## 解答2
数学法。我们用f(n,m)表示最后剩下那个数的索引号，每回去掉一个数，然后索引重置。我们需要找到f(n,m)和f(n-1,m)的关系。
* 去掉数为k=(m-1)%n（m可能比n大）
* 新的索引号x和原来的索引y的关系为y=(x+k+1)%n
* 于是有f(n,m)=(f(n−1,m)+k+1)%n
* 化简，f(n,m)=(f(n−1,m)+m)%n，且f(1,m)=0

时间复杂度：O(N), 空间复杂度: O(N)
```python
class Solution:
    def lastRemaining(self, n: int, m: int) -> int:
        if n == 1: return 0
        return (self.lastRemaining(n-1, m) + m) % n
```