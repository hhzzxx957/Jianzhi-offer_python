# 数据流中的中位数
剑指41 | [Link](https://leetcode-cn.com/problems/shu-ju-liu-zhong-de-zhong-wei-shu-lcof/)

## 题目
如何得到一个数据流中的中位数？如果从数据流中读出奇数个数值，那么中位数就是所有数值排序之后位于中间的数值。如果从数据流中读出偶数个数值，那么中位数就是所有数值排序之后中间两个数的平均值。

例如，

[2,3,4] 的中位数是 3

[2,3] 的中位数是 (2 + 3) / 2 = 2.5

设计一个支持以下两种操作的数据结构：

* void addNum(int num) - 从数据流中添加一个整数到数据结构中。
* double findMedian() - 返回目前所有元素的中位数。
```
示例 1：
输入：
["MedianFinder","addNum","addNum","findMedian","addNum","findMedian"]
[[],[1],[2],[],[3],[]]
输出：[null,null,null,1.50000,null,2.00000]

示例 2：
输入：
["MedianFinder","addNum","findMedian","addNum","findMedian"]
[[],[2],[],[3],[]]
输出：[null,null,2.00000,null,2.50000]

限制：
最多会对 addNum、findMedia进行 50000 次调用。
```

## 解答
用两个堆来实现这个操作。用小顶堆储存较大的一半数，大顶堆储存较小的那半。Python中heapq是小顶堆，大顶堆要通过变成负数实现。

时间复杂度：O(logN), 空间复杂度: O(N)
```python
from heapq import *
class MedianFinder:

    def __init__(self):
        """
        initialize your data structure here.
        """
        # small heap for bigger half, large heap for smaller half
        self.small, self.large = [], []


    def addNum(self, num: int) -> None:
        if len(self.small) != len(self.large):
            heappush(self.large, -heappushpop(self.small, num))
        else:
            heappush(self.small, -heappushpop(self.large, -num))

    def findMedian(self) -> float:
        if len(self.small) != len(self.large):
            return self.small[0]
        else:
            return (self.small[0]-self.large[0])/2.0



# Your MedianFinder object will be instantiated and called as such:
# obj = MedianFinder()
# obj.addNum(num)
# param_2 = obj.findMedian()
```