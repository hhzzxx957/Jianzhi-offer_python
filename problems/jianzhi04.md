#二维数组中的查找
剑指04 | [Link](https://leetcode-cn.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/)

## 题目
在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

```
示例:
现有矩阵 matrix 如下：
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
给定 target = 5，返回 true。
给定 target = 20，返回 false。

限制：
0 <= n <= 1000
0 <= m <= 1000
```

## 解答
把矩阵逆时针旋转45°，把右上角放到顶点，整个矩阵就像一个二叉搜索树。往左（col --）越来越小，往右(row++)越来越大。

时间复杂度：O(M+N), 空间复杂度: O(1)
```python
class Solution:
    def findNumberIn2DArray(self, matrix: List[List[int]], target: int) -> bool:
        if not matrix:
            return False
        
        m, n = len(matrix), len(matrix[0])
        rind, cind = 0, n-1
        while rind < m and cind >= 0:
            if matrix[rind][cind] < target:
                rind += 1
            elif matrix[rind][cind] > target:
                cind -= 1
            else:
                return True
        return False
```