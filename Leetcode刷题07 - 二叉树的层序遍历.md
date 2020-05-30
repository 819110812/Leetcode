# Leetcode刷题07 - 二叉树的层序遍历
给你一个二叉树，请你返回其按 层序遍历 得到的节点值。 （即逐层地，从左到右访问所有节点）。

示例：
```
二叉树：[3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回其层次遍历结果：

[
  [3],
  [9,20],
  [15,7]
]
```

我的解法：
```Python
def levelOrder(self, root: TreeNode) -> List[List[int]]:
        if not root : 
            return []
        arr , res = [root],[]
        while arr:
            temp = []
            temp_res = []
            for node in arr:
                temp_res.append(node.val)
                if node.left: temp.append(node.left)
                if node.right:temp.append(node.right)
            arr = temp
            res.append(temp_res)
        return res
```
广度优先遍历，但是很明显，这个写法的内存消耗很是严重啊。优化方法暂时还没想到，看到的很多写法都和这个类似，区别在于部分使用到了队列来实现，但是跑下来效果没差，hmmmm，优化方法暂且放到一边，待日后再整。
贴一波使用队列的方法：
```Python
def levelOrder(self, root):
		queue = collections.deque()
        queue.append(root)
        res = []
        while queue:
            size = len(queue)
            level = []
            for _ in range(size):
                cur = queue.popleft()
                if not cur:
                    continue
                level.append(cur.val)
                queue.append(cur.left)
                queue.append(cur.right)
            if level:
                res.append(level)
        return res

作者：fuxuemingzhu
链接：https://leetcode-cn.com/problems/binary-tree-level-order-traversal/solution/tao-mo-ban-bfs-he-dfs-du-ke-yi-jie-jue-by-fuxuemin/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```