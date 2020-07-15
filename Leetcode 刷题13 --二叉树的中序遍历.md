# Leetcode刷题13 --二叉树的遍历

给定一个二叉树，返回它的中序 遍历。

示例:

```
输入: [1,null,2,3]
   1
    \
     2
    /
   3

输出: [1,3,2]
```





解法1：借助辅助函数

```python
class Solution:
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        res = []
        if root is None:
            return res
        def bfs(root):
            if root is not None:
                dfs(root.left)
                res.append(root.val)
                dfs(root.right)

        dfs(root)
        return res
```



解法二：传统递归

```pytho
class Solution:
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        if root is None:
            return []
        if root is not None:
           return self.inorderTraversal(root.left) + [root.val] + self.inorderTraversal(root.right)

```



该方法虽然看起来简洁，但是运行时间比第一个多很多