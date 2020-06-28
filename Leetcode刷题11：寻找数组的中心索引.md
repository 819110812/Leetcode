# Leetcode刷题11：寻找数组的中心索引

给定一个整数类型的数组 nums，请编写一个能够返回数组 “中心索引” 的方法。

我们是这样定义数组 中心索引 的：数组中心索引的左侧所有元素相加的和等于右侧所有元素相加的和。

如果数组不存在中心索引，那么我们应该返回 -1。如果数组有多个中心索引，那么我们应该返回最靠近左边的那一个。

 

示例 1：

```
输入：
nums = [1, 7, 3, 6, 5, 6]
输出：3
解释：
索引 3 (nums[3] = 6) 的左侧数之和 (1 + 7 + 3 = 11)，与右侧数之和 (5 + 6 = 11) 相等。
同时, 3 也是第一个符合要求的中心索引。
```

示例 2：

```
输入：
nums = [1, 2, 3]
输出：-1
解释：
数组中不存在满足此条件的中心索引。
```



解法1：暴力破解，线性时间的遍历：

结果超时~~

方法很直白，计算左右的和，小白写法，但是这么写完全埋没了python的特点。这边有这个几个点写的很烂，

- 使用range和索引来 遍历，这么写很不方便，可以是用枚举的方法来写，也就是enumerate
- 这边还自己写了个sum的功能，重复造轮子，可以直接使用sum函数来实现
- 思路上很简单的，单纯的分别计算左右和，重复计算，降低效率

```
class Solution:
    def pivotIndex(self, nums: List[int]) -> int:
        for i in range(0,len(nums)):
            if self.compute_sum(nums,0,i) == self.compute_sum(nums,i+1,len(nums)):
                return i
        return -1
    
    def compute_sum(self,nums,start,end):
        res = 0
        for i in nums[start:end]:
            res+=i
        return res
            
```



解法2：

先计算出总和，遍历过程中动态计算左边的和，利用减法计算右侧的和，再比较。方法时间通过，但是内存有点小高

```
class Solution:
    def pivotIndex(self, nums: List[int]) -> int:
        total = sum(nums)
        leftsum =  0 
        for idx,i in enumerate(nums):
            if leftsum == (total-leftsum-i):
                return idx
            leftsum += i
        return -1
```





