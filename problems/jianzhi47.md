# 礼物的最大价值
剑指47 | [Link](https://leetcode-cn.com/problems/li-wu-de-zui-da-jie-zhi-lcof/)

## 题目
在一个 m*n 的棋盘的每一格都放有一个礼物，每个礼物都有一定的价值（价值大于 0）。你可以从棋盘的左上角开始拿格子里的礼物，并每次向右或者向下移动一格、直到到达棋盘的右下角。给定一个棋盘及其上面的礼物的价值，请计算你最多能拿到多少价值的礼物？
```
示例 1:
输入: 
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
输出: 12
解释: 路径 1→3→5→2→1 可以拿到最多价值的礼物

限制：
0 < grid.length <= 200
0 < grid[0].length <= 200
```

## 解答
2d的动态规划。记录所能拿到的最大价值。我们从左上往右下走(先列后行)，当前值是这个格的礼物值加上上或左中比较大的值。

时间复杂度：O(MN), 空间复杂度: O(1)
```python
class Solution:
    def maxValue(self, grid: List[List[int]]) -> int:
        i, j = 0, 0
        m, n = len(grid), len(grid[0])
        for i in range(1, m):
            grid[i][0] += grid[i-1][0]
        for j in range(1, n):
            grid[0][j] += grid[0][j-1]
        for i in range(1, m):
            for j in range(1, n):
                grid[i][j] += max(grid[i-1][j], grid[i][j-1])
        return grid[-1][-1]
```