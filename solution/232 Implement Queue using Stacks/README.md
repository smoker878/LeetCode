# [232. Implement Queue using Stacks](https://leetcode.com/problems/implement-queue-using-stacks/description/)

## 題目描述
用steak，創造Queue

## 解法1
![圖](img.svg)

```python3
class RecentCounter:
class MyQueue:

    def __init__(self):
        self.s1 = []
        self.s2 = []

    def push(self, x: int) -> None:
        self.s1.append(x)
        

    def pop(self) -> int:
        if not self.s2 : #s2是空的,s1移過去
            self.s2 = [self.s1[i] for i in range(len(self.s1)-1,-1,-1)]
            self.s1 = []        
        return self.s2.pop()


    def peek(self) -> int:
        if self.s2:
            return self.s2[-1]
        else:
            return self.s1[0] 


    def empty(self) -> bool:
        return not (self.s1 or self.s2)   
```
