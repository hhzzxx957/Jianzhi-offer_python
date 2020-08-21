# 重建二叉树
剑指07 | [Link](https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof/)

## 题目
输入某二叉树的前序遍历和中序遍历的结果，请重建该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。
```
示例:
前序遍历 preorder = [3,9,20,15,7]
中序遍历 inorder = [9,3,15,20,7]
返回如下的二叉树：
    3
   / \
  9  20
    /  \
   15   7
限制：
0 <= 节点个数 <= 5000
```

## 解答
* 在前序遍历里我们有[根，左，右]，于是可以得到根节点。
* 然后根据根节点（用哈希表查找），从中序遍历[左，右，根]中得到左右子树的个数。
* 构建in order的当前的根为节点
* 通过左右子树pre_order,in_left,in_right(都是指index)的关系构建root.left, root.right
* 递归直到中序遍历的list为空

初始化dictionary O(N). 递归建立N个节点，O(N)
时间复杂度: O(N), 空间复杂度: O(N)
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
        self.dic = {}
        self.preod = preorder
        for i, v in enumerate(inorder):
            self.dic[v] = i
        
        return self.recur(0,0,len(inorder)-1)

    def recur(self, pre_root, in_left, in_right):
        '''
        given preorder root, inorder left, right indices
        function to create treenode recursively
        '''
        if in_left > in_right: # inorder list is empty
            return        
        
        # find inorder root
        root = TreeNode(self.preod[pre_root])
        in_root = self.dic[root.val]

        # find the root of left tree through
        # new indices for left tree. Better to draw a picture
        root.left = self.recur(pre_root+1, in_left, in_root-1)
        # similar for right tree. 
        # 右子树根节点 = 根节点索引 + 左子树长度 + 1
        root.right = self.recur(in_root-in_left+pre_root+1, in_root+1, in_right)

        return root
```