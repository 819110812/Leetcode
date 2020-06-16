# Leetcode刷题10 -- 从尾到头打印链表
输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。


示例 1：
```
输入：head = [1,3,2]
输出：[2,3,1]
```

解法1： 暴力遍历+列表倒置

```Python
class Solution:
    def reversePrint(self, head: ListNode) -> List[int]:
        if head is None:
            return []
        res = []
        cur = head
        while cur:
            res.append(cur.val)
            cur = cur.next
        return res[::-1]
```

解法2：递归

函数功能，返回下一个值+当前值
判别条件：是否存在head，没有就为空
```Python
class Solution:
    def reversePrint(self, head: ListNode) -> List[int]:
        return self.reversePrint(head.next) + [head.val] if head else []
```