# 包含min函数的栈
剑指30 | [Link](https://leetcode-cn.com/problems/bao-han-minhan-shu-de-zhan-lcof/)

## 题目
定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。
```
示例:
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.min();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.min();   --> 返回 -2.

限制,
各函数的调用总次数不超过 20000 次
```

## 解答
用两个栈来存储，用一个栈专门存储当前最小值。每当有更小（<=）的值输入的时候，就append到这里。pop的时候如果和当前最小值相同一同pop出去。

时间复杂度：O(1), 空间复杂度: O(N)
```python
class MinStack:

    def __init__(self):
        """
        initialize your data structure here.
        """
        self.stack = []
        self.minnums = [float('inf')] # 放一个最小值方便比较。

    def push(self, x: int) -> None:
        self.stack.append(x)
        if x <= self.minnums[-1]: self.minnums.append(x)

    def pop(self) -> None:
        if self.stack.pop() == self.minnums[-1]:
            self.minnums.pop()
        
    def top(self) -> int:
        return self.stack[-1]

    def min(self) -> int:
        return self.minnums[-1]
```