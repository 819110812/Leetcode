# Leetcode刷题14 --- 判断能否形成等差数列

给你一个数字数组 arr 。

如果一个数列中，任意相邻两项的差总等于同一个常数，那么这个数列就称为 等差数列 。

如果可以重新排列数组形成等差数列，请返回 true ；否则，返回 false 。

 

示例 1：

```
输入：arr = [3,5,1]
输出：true
解释：对数组重新排序得到 [1,3,5] 或者 [5,3,1] ，任意相邻两项的差分别为 2 或 -2 ，可以形成等差数列。
示例 2：

输入：arr = [1,2,4]
输出：false
解释：无法通过重新排序得到等差数列。
```



解法1： 朴素的解法，先排序，然后通过减法判断是否差相等。

```
class Solution:
    def canMakeArithmeticProgression(self, arr: List[int]) -> bool:
        if len(arr)<=2:
            return True
        arr.sort()
        p = 1 #定义了一个从位置1开始的指针
        while p+1<len(arr):
            if arr[p]-arr[p-1] != arr[p+1]-arr[p]: # 判断是否等差
                return False
            p+=1
        return True
```



解法2: 利用了等差数列的性质，`` arr[i] * 2 != arr[i - 1] + arr[i + 1]``

```
class Solution:
    def canMakeArithmeticProgression(self, arr: List[int]) -> bool:
        arr.sort()
        for i in range(1, len(arr) - 1):
            if arr[i] * 2 != arr[i - 1] + arr[i + 1]:
                return False
        return True
```



