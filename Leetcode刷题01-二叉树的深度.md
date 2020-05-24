# Leetcode刷题记录01-二叉树的深度
输入一棵二叉树的根节点，求该树的深度。从根节点到叶节点依次经过的节点（含根、叶节点）形成树的一条路径，最长路径的长度为树的深度。

例如：

给定二叉树 [3,9,20,null,null,15,7]，
```
    3
   / \
  9  20
    /  \
   15   7
```
返回它的最大深度 3 。

### *Python解法*
1. 深度优先遍历
```
    def maxDepth(self, root: TreeNode) -> int:
        if root is None:
            return 0
        return max(self.maxDepth(root.left),self.maxDepth(root.right))+1  #比较左右子树哪个最深
```
2. 广度优先遍历
使用一个列表和计数器来遍历整个二叉树，每遍历一次计数器加1，并将列表更新
```
def maxDepth(self, root: TreeNode) -> int:
        if root is None:
            return 0
        arr,res = [root],0
        while arr:
            temp = []
            for node in arr:
                if node.left :temp.append(node.left)
                if node.right: temp.append(node.right)
            arr = temp
            res+=1
        return res
```
广度优先的方法利用的空间去置换出了递归时的时间，使得遍历更快

再用Java语言将二者实现一遍

2.Java版
写法一致，只是用来当做学习Java的一个途径
*DFS*
```
class Solution {
    public int maxDepth(TreeNode root) {
        if(root==null){
            return 0;
        }
        return Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
    }
}
```
*BFS*
```
class Solution {
    public int maxDepth(TreeNode root) {
        if(root == null) return 0;
        List<TreeNode> arr = new ArrayList<>() {{ add(root); }}, tmp;
        int res = 0;
        while(!arr.isEmpty()) {
            tmp = new LinkedList<>();
            for(TreeNode node : arr) {
                if(node.left != null) tmp.add(node.left);
                if(node.right != null) tmp.add(node.right);
            }
            arr = tmp;
            res++;
        }
        return res;
    }
}
```