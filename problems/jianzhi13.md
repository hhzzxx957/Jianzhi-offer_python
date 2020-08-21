# 机器人的运动范围
剑指13 | [Link](https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/)

## 题目
地上有一个m行n列的方格，从坐标 [0,0] 到坐标 [m-1,n-1] 。一个机器人从坐标 [0, 0] 的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于k的格子。例如，当k为18时，机器人能够进入方格 [35, 37] ，因为3+5+3+7=18。但它不能进入方格 [35, 38]，因为3+5+3+8=19。请问该机器人能够到达多少个格子？

```
示例 1：
输入：m = 2, n = 3, k = 1
输出：3

示例 2：
输入：m = 3, n = 1, k = 0
输出：1

限制：
1 <= n,m <= 100
0 <= k <= 20
```

## 解答
dfs遍历，每次向右或者向下走，注意不要重复访问。用一个set记录已经拜访过的位置的索引。

时间复杂度：O(MN)， 空间复杂度: O(MN)
```python
class Solution:
    def movingCount(self, m: int, n: int, k: int) -> int:
        self.m, self.n, self.k = m,n,k
        self.count, visited = 0, set()
        self.dfs(0, 0, 0, 0, visited)
        return self.count
    
    def digitssum(self, num):
        ssum = 0
        while num > 0:
            ssum += num%10
            num //= 10
        return ssum

    def dfs(self, i, j, si, sj, visited):
        if not 0 <= i < self.m or not 0 <= j < self.n: return
        if si + sj > self.k or (i, j) in visited: return
        
        visited.add((i,j))
        self.count += 1

        self.dfs(i+1,j,self.digitssum(i+1), sj, visited) 
        self.dfs(i,j+1,si,self.digitssum(j+1), visited)
```
## 解答2
用bfs遍历。用一个队列来储存索引和对应的数字和。
```python
class Solution:
    def movingCount(self, m: int, n: int, k: int) -> int:
        queue, visited = collections.deque(), set()
        queue.append((0,0,0,0))
        while queue:
            i,j,si,sj = queue.popleft()
            if not 0 <= i < m or not 0 <= j < n: continue
            if si + sj > k or (i, j) in visited: continue
            visited.add((i,j))
            queue.append((i+1,j,self.digitssum(i+1),sj))
            queue.append((i,j+1,si,self.digitssum(j+1)))
        return len(visited)
    
    def digitssum(self, num):
        ssum = 0
        while num > 0:
            ssum += num%10
            num //= 10
        return ssum
```