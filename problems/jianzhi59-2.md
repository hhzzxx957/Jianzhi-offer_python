# 队列的最大值
剑指59-2 | [Link](https://leetcode-cn.com/problems/dui-lie-de-zui-da-zhi-lcof/)

## 题目
请定义一个队列并实现函数 max_value 得到队列里的最大值，要求函数max_value、push_back 和 pop_front 的均摊时间复杂度都是O(1)。

若队列为空，pop_front 和 max_value 需要返回 -1
```
示例 1：
输入: 
["MaxQueue","push_back","push_back","max_value","pop_front","max_value"]
[[],[1],[2],[],[],[]]
输出: [null,null,null,2,1,2]

示例 2：
输入: 
["MaxQueue","pop_front","max_value"]
[[],[],[]]
输出: [null,-1,-1]

限制：
1 <= push_back,pop_front,max_value的总操作数 <= 10000
1 <= value <= 10^5
```

## 解答
通过辅助队列实现O(1)取max的操作。辅助队列储存局部最大值。

时间复杂度：O(1), 空间复杂度: O(N)
```python
class MaxQueue:

    def __init__(self):
        self.deque = collections.deque()
        self.maxque = collections.deque()

    def max_value(self) -> int:
        if not self.maxque: return -1
        else:
            return self.maxque[0]

    def push_back(self, value: int) -> None:
        while self.maxque and self.maxque[-1] < value:
            self.maxque.pop()
        self.maxque.append(value)
        self.deque.append(value)

    def pop_front(self) -> int:
        if not self.deque: return -1
        if self.deque[0] == self.maxque[0]:
            self.maxque.popleft()
        return self.deque.popleft()



# Your MaxQueue object will be instantiated and called as such:
# obj = MaxQueue()
# param_1 = obj.max_value()
# obj.push_back(value)
# param_3 = obj.pop_front()
```