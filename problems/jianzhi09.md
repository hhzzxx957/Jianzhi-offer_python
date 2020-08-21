# 用两个栈实现队列
剑指09 | [Link](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)

## 题目
用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )


```
示例1:
输入：
["CQueue","appendTail","deleteHead","deleteHead"]
[[],[3],[],[]]
输出：[null,null,3,-1]

示例2:
输入：
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
[[],[],[5],[2],[],[]]
输出：[null,-1,null,null,5,2]

限制：
1 <= values <= 10000
最多会对 appendTail、deleteHead 进行 10000 次调用
```

## 解答
用两个栈来实现倒序

时间复杂度：O(1), 空间复杂度: O(N)
```python
class CQueue:
    def __init__(self):
    # list B 用于储存倒序
        self.A, self.B = [], []

    def appendTail(self, value: int) -> None:
        self.A.append(value)

    def deleteHead(self) -> int:
        if self.B:
            return self.B.pop()
        else:
            if not self.A: # 没有数字
                return -1
            else:
                while self.A: # 把A中数字都倒序放到B
                    self.B.append(self.A.pop())
            return self.B.pop()


# Your CQueue object will be instantiated and called as such:
# obj = CQueue()
# obj.appendTail(value)
# param_2 = obj.deleteHead()
```