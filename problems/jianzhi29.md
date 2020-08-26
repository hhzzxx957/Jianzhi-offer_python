# 顺时针打印矩阵
剑指29 | [Link](https://leetcode-cn.com/problems/shun-shi-zhen-da-yin-ju-zhen-lcof/)

## 题目
输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。
```
示例 1：
输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
输出：[1,2,3,6,9,8,7,4,5]

示例 2：
输入：matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
输出：[1,2,3,4,8,12,11,10,9,5,6,7]
 
限制：
0 <= matrix.length <= 100
0 <= matrix[i].length <= 100
```

## 解答
模拟数字运动方式一圈一圈转。没走完一条边就把相应的边界值+/-1。左后一圈可能超出范围，所以可以加一个判断条件，或者对结果切片。

时间复杂度：O(MN), 空间复杂度: O(MN)
```python
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        if not matrix: return []
        res = []
        r_edge = [0, len(matrix)-1]
        c_edge = [0, len(matrix[0])-1]
        while len(res) < len(matrix)*len(matrix[0]):
            # top row
            for j in range(c_edge[0],c_edge[1]+1):
                res.append(matrix[r_edge[0]][j])
            r_edge[0]+=1
            # right column
            for i in range(r_edge[0],r_edge[1]+1):
                res.append(matrix[i][c_edge[1]])
            c_edge[1]-=1
            # bottom row
            for j in range(c_edge[1],c_edge[0]-1,-1):
                res.append(matrix[r_edge[1]][j])
            r_edge[1]-=1
            # left column
            for i in range(r_edge[1],r_edge[0]-1,-1):
                res.append(matrix[i][c_edge[0]])
            c_edge[0]+=1
        return res[:len(matrix)*len(matrix[0])]
```