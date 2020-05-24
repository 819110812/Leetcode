# Leetcode刷题03-对称二叉树
请实现一个函数，用来判断一棵二叉树是不是对称的。如果一棵二叉树和它的镜像一样，那么它是对称的。

例如，二叉树 [1,2,2,3,4,4,3] 是对称的。
```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```
但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:
```
    1
   / \
  2   2
   \   \
   3    3
```


示例 1：
```
输入：root = [1,2,2,3,4,4,3]
输出：true
```
示例 2：
```
输入：root = [1,2,2,null,3,null,3]
输出：false
```

来源：力扣（LeetCode）
链接：[https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof](https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof)

题目要求判断一个二叉树是否平衡，看到二叉树，第一想到的是递归，然后是深度优先或者广度优先。在构建递归方法，三步走，
1.确定我们的递归程序的功能：判断是否对称，则返回值是false 或者是true
2.函数的输入是什么？
root.left,root.right. 为什么？ 我的理解是，因为要判断是否对称，那就要输入两边的子树进行比较，如果只是单独的root,递归过程很难去判断
3. 何时终止/边界条件？
如果都空，则完全一样，返回true,如果传入的左右节点有一个是空的，则不对称，则返回false。 
此外还要实现判断对称的过程，即，传入的两节点值一样，且（1）左节点的左子树值等于右节点的右子树值，（2） 左节点的右子树值等于右节点的左子树值

先贴一下本菜鸡的实现方法：
```
def isSymmetric(self, root: TreeNode) -> bool:
        if not root:
            return True
        def dfs(left,right):
            if not left and not right:
                return True
            if not left or not right:
                return False
            return left.val==right.val and dfs(left.left,right.right) and dfs(left.right,right.left) 
        return dfs(root.left,root.right)
```
定义了一个辅助函数对传入节点进行判断并进行递归。
下面是官方的写法：
```
def isSymmetric(self, root: TreeNode) -> bool:
        def recur(L, R):
            if not L and not R: return True
            if not L or not R or L.val != R.val: return False
            return recur(L.left, R.right) and recur(L.right, R.left)

        return recur(root.left, root.right) if root else True
```
作者：jyd
链接：[https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof/solution/mian-shi-ti-28-dui-cheng-de-er-cha-shu-di-gui-qing/](https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof/solution/mian-shi-ti-28-dui-cheng-de-er-cha-shu-di-gui-qing/)
来源：力扣（LeetCode）

思路大致相同，但是官方的显得更加简单干练，将Python语言特性发挥的淋漓尽致。

大致总结一下思路过程：
看到二叉树，想到要去写个递归，然后考虑这个递归的要素怎么设计，递归的主要实现，最后再去优化。