# Leetcode刷题06--二分查找
刷一道经典的算法，二分查找，虽然是经典算法但是有很多细节在写的时候也是要注意的，不经意间可能就会少加个1多加个1

给定一个 n 个元素有序的（升序）整型数组 nums 和一个目标值 target  ，写一个函数搜索 nums 中的 target，如果目标值存在返回下标，否则返回 -1。


示例 1:
```
输入: nums = [-1,0,3,5,9,12], target = 9
输出: 4
解释: 9 出现在 nums 中并且下标为 4
```
示例 2:
```
输入: nums = [-1,0,3,5,9,12], target = 2
输出: -1
解释: 2 不存在 nums 中因此返回 -1
```

解法1：
传统二分查找
```Python
def search(self, nums: List[int], target: int) -> int:
		left,right = 0,len(nums)-1
		while left<=right:
			mid = (right+left)//2  # 地板除
			if target< nums[mid]: right = mid-1 #如果小于，则说明目标值出现在mid的左侧
			elif target > nums[mid]: left = mid+1 #如果大于，则说明目标出现在mid的右侧
			else: return mid # 如果等于，直接返回mid，就是我们要的目标索引
		return	-1 #不存在就返回-1

```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200530135114938.png)
运行的效率不是很高。当然也可以用抖机灵的方法来实现：

解法2：
```Python
def search(self, nums: List[int], target: int) -> int:
		if target in nums:
			return nums.index(target)
		eles:
			return -1
```
这种方法，简洁，但是效率不高，因为你有一个``in``操作这个是O（n）的时间复杂度。