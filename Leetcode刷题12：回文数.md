## Leetcode刷题12：回文数

判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

示例 1:

```
输入: 121
输出: true
```



示例 2:

```
输入: -121
输出: false
解释: 从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。
```


示例 3:

```
输入: 10
输出: false
解释: 从右向左读, 为 01 。因此它不是一个回文数。
```





方法1： 各种类型转换，体现python内置函数的强大，但是运行时间和内存消耗会很严重，毕竟每个函数背后都是满满的损耗啊，随手一写，没有考虑很多，不赞成这种写法，很不优雅

```python
class Solution:
    def isPalindrome(self, x: int) -> bool:
        if list(str(x)) == list(str(x))[::-1]:
            return True
        else:
            return False
```



方法2：

仔细分析一下题目，可以看出，当输入的是负数是可以提前结束，所以 ``x<0`` 时可以直接返回``False``.同时，当尾数是0的时候，也是``False`。由此可以写出提前结束条件为：

```python
if x<0 or (x%10==0 and x!=0): return False
```

接下来就是将数字进行回文处理，这边要注意的就是判断``True``的时候要考虑原始的整数是奇数个数字还是偶数个数字，因为我们要将数字进行一半的翻转，奇数个和偶数个会相差以为，所以最后的时候我们要判断两种情况，一个是``reversed == x`` 另一个就是将翻转后的数去掉一位 ``x==reversed//10``.

这边还有一点就是，我们用的是``//``而不是``/``，前者是整数除，后者是浮点除，结果是不一样的。完整的代码是

```python
class Solution:
    def isPalindrome(self, x: int) -> bool:
        if x < 0 or (x % 10 == 0 and x != 0): return False 
        if x== 0: return True    
        reserved = 0
        while x > reserved:
            reserved = reserved*10 + x%10
            x = x//10
        print(reserved)
        print(x)
        return x == reserved or x == reserved // 10
```

这次的运行时间会比上面的好上很多。