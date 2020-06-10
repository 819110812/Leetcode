# Leetcode刷题09--二维数组中的查找
在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

 

示例:
```
现有矩阵 matrix 如下：

[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```
给定 target = 5，返回 ``true``。

给定 target = 20，返回`` false``。

这题用Python写就很无聊了，这次直接放java的写法
```Java
class Solution {
    public boolean findNumberIn2DArray(int[][] matrix, int target) {
        if(matrix.length==0 || matrix == null){
            return false;
        }
        int m = matrix.length,n = matrix[0].length;
        int row =0,col = n-1;
        while (row<m && col>=0){
            int num = matrix[row][col];  // 从矩阵的右上角开始的遍历，这样子好比较大小
            if(num==target){
                return true;
            }else if(num<target){ //目标数大于当前数的话，说明我们的目标数应该在下一行，因为我们是从后面马开始比较的
                row++;
            }else{ //反之，则在当前行的左边
                col--;
            }
        }
        return false;
    }
}

```