# Leetcode刷题04-股票的最大利润
假设把某股票的价格按照时间先后顺序存储在数组中，请问买卖该股票一次可能获得的最大利润是多少？

示例 1:
```
输入: [7,1,5,3,6,4]
输出: 5
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，
最大利润 = 6-1 = 5 。 注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格。
```
示例 2:
```
输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```
一看到这题，第一反应就是动态规划，为什么是动态规划呢？因为这题是就最值，一般求最值问题，动态规划来解会得心应手。既然是动态规划，那么就要考虑到我们的状态转移方程是什么。
从题目中可以得到这么一个信息，股票是低买高卖，那么就需要记录下一个极小值，并且要做一个取舍，当前的价格减去最小值的利润是否比之前的最大利润多。
大致的一个思路就是这样，那么我们的状态转移方程则是：
```
dp[i] = max(prices[i]-temp,dp[i-1])
```
dp[i] 则是记录我们的当前最大值， max(prices[i]-temp,dp[i-1])则是在取最大的情况存进我们的dp列表中。
完整的代码是这样的：
```Python
from typing import List


class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        dp = [0]*len(prices)  # 初始化我们的dp列表
        temp = prices[0] #将第一天的价格记做暂时的最小值
        for i in range(1,len(prices)):
            if prices[i]<=temp: #如果有更小的则更新
                temp = prices[i]
            dp[i] = max(prices[i]-temp,dp[i-1])
        return dp[len(prices)-1] #返回最终的结果 



if __name__ == '__main__':
    stock = [7,6,4,3,1]
    sol = Solution()
    print(sol.maxProfit(stock)) #返回5
```
上面的写法算是很中规中矩的动态规划写法，来看下官方给出的解法
```Python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        cost, profit = float("+inf"), 0
        for price in prices:
            cost = min(cost, price)
            profit = max(profit, price - cost)
        return profit

作者：jyd
链接：https://leetcode-cn.com/problems/gu-piao-de-zui-da-li-run-lcof/solution/mian-shi-ti-63-gu-piao-de-zui-da-li-run-dong-tai-2/
来源：力扣（LeetCode）
```
基本思路是一致的，都是记录下当前的最小值和最大利润，然后计算判断，不过官方的明显要比我自己写的简练很多，hmmmm，还有好多要走呢，奥利给！