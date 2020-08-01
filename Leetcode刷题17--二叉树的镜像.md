# Leetcode刷题17--二叉树的镜像

请完成一个函数，输入一个二叉树，该函数输出它的镜像。

例如输入：

     	4
      /   \
      2     7
     / \   / \
    1   3 6   9

镜像输出：

```
	 4
   /   \
  7     2
 / \   / \
9   6 3   1
```

​	



示例 1：

输入：root = [4,2,7,1,3,6,9]
输出：[4,7,2,9,6,3,1]



很简单，设计一个递归，将左右子树对换

一定要同时赋值，否则会重复，或者使用一个temp中间变量

```python
class Solution:
    def mirrorTree(self, root: TreeNode) -> TreeNode:
        if root is None:
            return root
        if root:
            root.left,root.right = self.mirrorTree(root.right),self.mirrorTree(root.left)
        return root
```

