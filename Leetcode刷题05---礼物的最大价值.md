# Leetcode刷题05---礼物的最大价值
本题来自剑指offer的47题

在一个 m*n 的棋盘的每一格都放有一个礼物，每个礼物都有一定的价值（价值大于 0）。你可以从棋盘的左上角开始拿格子里的礼物，并每次向右或者向下移动一格、直到到达棋盘的右下角。给定一个棋盘及其上面的礼物的价值，请计算你最多能拿到多少价值的礼物？

 

示例 1:
```
输入: 
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
输出: 12
解释: 路径 1→3→5→2→1 可以拿到最多价值的礼物
```
分析一下解题思路，这个题目的类型很明确，求极值，只不过加了一点类似路径的内容，本质还是一个求极值的问题，那么就立马想到用动态规划去做。将问题细分至最小子问题，我们要求最值，那么在最后一个时刻的最值就应该是由前一时刻的最大值+当前的值。那么状态转移方程就是 `` dp[i][j] = max(dp[i][j-1],dp[i-1][j]) + grid[i][j]``，这么直接写进去会出现一个问题，就是边界值的问题，在边界的处理上需要做一些额外的判断，我们可以直接将我们的dp矩阵扩张一下，为什么这么做呢？因为我们要考虑到左上角的情况，这个时候 i,j都是0，为了解决这个问题我们可以将遍历的范围从1开始计，那么dp[1]][1] 就对应了grid[0][0]的值，所以在写的时候 应该是 `` dp[i][j] = max(dp[i][j-1],dp[i-1][j])+grid[i-1][j-1]``。同时我们的遍历范围也需要跟着扩展，完整的代码是
```Python
class Solution:
    def maxValue(self, grid: List[List[int]]) -> int:
       dp = [[0]*(len(grid[0])+1)]*(len(grid)+1)
       for i in range(1,len(grid)+1):
           for j in range(1,len(grid[0])+1):
               dp[i][j] = max(dp[i][j-1],dp[i-1][j])+grid[i-1][j-1]
        return dp[-1][-1]


if __name__ == '__main__':
    arr = [[1,2,5],[3,2,1]]
    sol = Solution()
    print(sol.maxValue(arr)) #返回9  dp矩阵为[[0, 4, 6, 9], [0, 4, 6, 9], [0, 4, 6, 9]]

```
整体代码，额外空间 O（mn），时间O（mn）
日常看一眼官方给出的代码：
```Python
class Solution:
    def maxValue(self, grid: List[List[int]]) -> int:
        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if i == 0 and j == 0: continue
                if i == 0: grid[i][j] += grid[i][j - 1]
                elif j == 0: grid[i][j] += grid[i - 1][j]
                else: grid[i][j] += max(grid[i][j - 1], grid[i - 1][j])
        return grid[-1][-1]

作者：jyd
链接：https://leetcode-cn.com/problems/li-wu-de-zui-da-jie-zhi-lcof/solution/mian-shi-ti-47-li-wu-de-zui-da-jie-zhi-dong-tai-gu/
来源：力扣（LeetCode）

```
解释性很强，考虑了很细致的情况
- 通用情况： 数值不在边界上，那么就是它的上面一个元素和左边一个元素比大小，取最大的和自己相加，即 `` max(dp[i-1] [j],dp[i][j-1])+grid[i][j]`` 
- 考虑到边界情况，如果是第一个点，即左上角那个点，则是直接赋值：`` dp[i][j]=0``
- 如果在第一行，则只能在左边寻找到极值， 即 `` dp[i][j] = dp[i][j-1]+grid[i][j]``
- 如果在第一列却不在第一行，就是在最左边的边边上，我们的极值就是上面那个元素，即 ``dp[i][j] = dp[i-1][j]+grid[i][j]``
很妙的是，这边用的原地修改，这样额外空间就不会很大。
```Python
class Solution:
    def maxValue(self, grid: List[List[int]]) -> int:
        m, n = len(grid), len(grid[0])
        for j in range(1, n): # 初始化第一行
            grid[0][j] += grid[0][j - 1]
        for i in range(1, m): # 初始化第一列
            grid[i][0] += grid[i - 1][0]
        for i in range(1, m):
            for j in range(1, n):
                grid[i][j] += max(grid[i][j - 1], grid[i - 1][j])
        return grid[-1][-1]

作者：jyd
链接：https://leetcode-cn.com/problems/li-wu-de-zui-da-jie-zhi-lcof/solution/mian-shi-ti-47-li-wu-de-zui-da-jie-zhi-dong-tai-gu/
来源：力扣（LeetCode）
```
这是官方给出的第二种解法，提前初始化，减少了判断的冗余，hmmmm，妙啊！
回顾一下自己的写法，相比之下，解释性不是那么的通俗易懂，额外空间偏大。