# Leetcode刷题19--地图分析

你现在手里有一份大小为 N x N 的 网格 grid，上面的每个 单元格 都用 0 和 1 标记好了。其中 0 代表海洋，1 代表陆地，请你找出一个海洋单元格，这个海洋单元格到离它最近的陆地单元格的距离是最大的。

我们这里说的距离是「曼哈顿距离」（ Manhattan Distance）：(x0, y0) 和 (x1, y1) 这两个单元格之间的距离是 |x0 - x1| + |y0 - y1| 。

如果网格上只有陆地或者海洋，请返回 -1。

 

示例 1：

|   1   |   1   |   0   |
| :---: | :---: | :---: |
| **0** | **0** | **0** |
| **1** | **1** | **0** |

```
输入：[[1,0,1],[0,0,0],[1,0,1]]
输出：2
解释： 
海洋单元格 (1, 1) 和所有陆地单元格之间的距离都达到最大，最大距离为 2。
```



示例 2：

|   1   |   0   |   0   |
| :---: | :---: | :---: |
| **0** | **0** | **0** |
| **0** | **0** | **0** |

```
输入：[[1,0,0],[0,0,0],[0,0,0]]
输出：4
解释： 
海洋单元格 (2, 2) 和所有陆地单元格之间的距离都达到最大，最大距离为 4。
```





解法： 广度优先遍历，先入队每个陆地的位置，然后对每个陆地向外扩张，对每个访问过的点原地修改数值。

```python
class Solution:
    def maxDistance(self, grid: List[List[int]]) -> int:
        from collections import deque
        length = len(grid)
        temp_dequeue = deque()
        for row in range(length):
            for col in range(length):
                if grid[row][col]==1: #将所有陆地入队
                    temp_dequeue.append([row,col])
        # 此时队列中存的是所有陆地的坐标位置
        hasOcean = False
        temp_point= None
        while temp_dequeue:
            temp_point = temp_dequeue.popleft()
            x,y = temp_point #当前陆地的位置
            #对当前的点进行上下所有的移动
            for x_dir,y_dir in [[-1,0],[0,1],[1,0],[0,-1]]:
                new_x = x+x_dir
                new_y = y+y_dir
                if new_x<0 or new_x>=length or new_y<0 or new_y>=length or grid[new_x][new_y]!=0:
                   #到达边界了或者是已经访问过了
                    continue
                grid[new_x][new_y] = grid[x][y]+1 #原地修改，表示已经访问过了 数值+1
                hasOcean = True
                temp_dequeue.append([new_x,new_y])
        if temp_point==[] or not hasOcean: #如果说没有一个海洋，肯定是-1
                return -1
        else:
            return grid[temp_point[0]][temp_point[1]]-1
```



