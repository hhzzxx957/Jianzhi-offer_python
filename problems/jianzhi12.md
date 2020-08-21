# 矩阵中的路径
剑指12 | [Link](https://leetcode-cn.com/problems/ju-zhen-zhong-de-lu-jing-lcof/)

## 题目
请设计一个函数，用来判断在一个矩阵中是否存在一条包含某字符串所有字符的路径。路径可以从矩阵中的任意一格开始，每一步可以在矩阵中向左、右、上、下移动一格。如果一条路径经过了矩阵的某一格，那么该路径不能再次进入该格子。例如，在下面的3×4的矩阵中包含一条字符串“bfce”的路径。
```
[["a","b","c","e"],
["s","f","c","s"],
["a","d","e","e"]]
```
但矩阵中不包含字符串“abfb”的路径，因为字符串的第一个字符b占据了矩阵中的第一行第二个格子之后，路径不能再次进入这个格子。

```
示例 1：
输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
输出：true

示例 2：
输入：board = [["a","b"],["c","d"]], word = "abcd"
输出：false

限制：
1 <= board.length <= 200
1 <= board[i].length <= 200
```

## 解答
使用深度优先遍历dfs和剪枝。经过的数字用'#'代替，避免再次访问。

M,N：矩阵行列长度，K：字符串长度
可能有MN个起始点，每次有三个方向进行下一步3<sup>K</sup>。每次递归深度不超过K次。

时间复杂度：O(3<sup>K</sup>MN), 空间复杂度: O(K)
```python
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        m, n = len(board), len(board[0])
        for i in range(m):
            for j in range(n):
                if self.dfs(board, i, j, 0, word):
                    return True
        return False

    def dfs(self, board, i, j, wordind, word):
        if not 0 <= i < len(board) or not 0 <= j < len(board[0]):
            return False
        if board[i][j] != word[wordind]:
            return False

        if wordind == len(word) - 1:
            return True
        
        temp, board[i][j] = board[i][j], '#'

        di, dj = [0, -1, 0, 1], [-1, 0, 1, 0] #对应左下右上
        for k in range(4):
            if self.dfs(board, i+di[k], j+dj[k], wordind+1, word):
                return True

        board[i][j] = temp
        return False
```