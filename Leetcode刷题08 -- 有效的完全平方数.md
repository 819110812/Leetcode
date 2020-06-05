# Leetcode刷题08 -- 有效的完全平方数
给定一个正整数 num，编写一个函数，如果 num 是一个完全平方数，则返回 True，否则返回 False。

说明：不要使用任何内置的库函数，如  sqrt。

示例 1：
```
输入：16
输出：True
```
示例 2：
```
输入：14
输出：False
```
看到这个题目的，第一反应是用二分法，为什么是二分法呢? 因为平方数的这个特殊的属性，是同一个数的相乘，那么用二分来逼近就很符合这个场景。
解法1： 二分法：
```Python
def isPerfectSquare(self, num: int) -> bool:
        left,right = 0,num
        while left<=right:
            mid = (left+right)//2
            if mid*mid > num: right=mid-1
            elif mid*mid <num: left = mid+1
            else: return True
        return False
```
Java 写法，这边有点不同，就是中值的计算
```Java
class Solution {
    public boolean isPerfectSquare(int num) {
        long left=0;
        long right=num;
        while(left<=right){
            long mid = left+(right-left)/2;
            if(mid*mid==num){
                return true;
            }
            if(mid*mid>num){
                right = mid-1;
            }else{
                left = mid+1;
            }
        }
        return false;
    }
}
```

解法二，在看到官方解法的时候，突然想到了机器学习中的牛顿法，附上一个牛顿法的讲解 （https://zhuanlan.zhihu.com/p/46536960），大致的思想就是从一个初始值开始，作一系列改进的逼近根的过程。
```python
def isPerfectSquare(self, num: int) -> bool:
        if num < 2:
            return True
        
        x = num // 2
        while x * x > num:
            x = (x + num // x) // 2
        return x * x == num

作者：LeetCode
链接：https://leetcode-cn.com/problems/valid-perfect-square/solution/you-xiao-de-wan-quan-ping-fang-shu-by-leetcode/
```