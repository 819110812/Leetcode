# Leetcode 平衡二叉树
1. 什么是平衡二叉树（Balanced Binary Tree）
二叉树是一种二叉排序树，它的左右子树的高度不得超过一。这是这题的关键，至于树的维护，本文不会加以描述
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020052220375832.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzk0MzY0Mg==,size_16,color_FFFFFF,t_70)
[图片来源：百度图片]

2. 基本思路
遇到二叉树的问题基本就是DFS，BFS走一波试试，这题采用了一个DFS的辅助函数，遍历过后计算树的高度
辅助函数：
```
def dfs(root):
	if not root: return 0
    return max(dfs(root.left), dfs(root.right)) + 1 #计算树的高度
```
很明显的可以看dfs的功能就是来计算树的一个高度。结合原先的函数，完整的代码就是：
```
class Solution:
    def isBalanced(self, root: TreeNode) -> bool:
        if root is None:
            return True

        def dfs(root):
            if not root: return 0
            return max(dfs(root.left), dfs(root.right)) + 1

        return abs(dfs(root.left) - dfs(root.right)) <=1 and self.isBalanced(root.left) and self.isBalanced(root.right)
```
如果是空树，则为True,必然是平衡树。
返回需要以下条件同时成立：

- 当前子树是平衡树 即（abs(dfs(root.left) - dfs(root.right)) <=1）
- 左子树是平衡树 即  self.isBalanced(root.left)
- 右子树是平衡树 即 self.isBalanced(root.right)

提交的结果运行时间不是很优秀，还有待改善！