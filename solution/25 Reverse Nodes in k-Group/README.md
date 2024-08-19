# [25. Reverse Nodes in k-Group](https://leetcode.com/problems/reverse-nodes-in-k-group/description/)

## 題目描述
* 一個鏈表，每經過k個節點，就將前面幾個節點翻轉一次
  ![圖](https://assets.leetcode.com/uploads/2020/10/03/reverse_ex1.jpg)

## 解法
* 用一個steak，存要翻轉的數字
* 當steak為空時，紀錄左邊的節點
* 當steak長度等於k時，開始翻轉
* 翻轉：steak每pop一個數字，就附值給left，然後left前進一次
  

```python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseKGroup(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        cur = head
        steak = []
        while cur:
            if len(steak) == 0:  #當steak為空時，紀錄左邊的節點
                left = cur
            steak.append(cur.val)
            if len(steak) == k: #當steak長度等於k時，開始翻轉
                while steak:
                    left.val = steak.pop()
                    left = left.next
            cur = cur.next
        return head  
```
