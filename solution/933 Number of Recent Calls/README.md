# [933. Number of Recent Calls](https://leetcode.com/problems/number-of-recent-calls/description/)

## 題目描述
You have a RecentCounter class which counts the number of recent requests within a certain time frame.

Implement the RecentCounter class:

* RecentCounter() Initializes the counter with zero recent requests.
int ping(int t) Adds a new request at time t, where t represents some time in milliseconds, and returns the number of requests that has happened in the past 3000 milliseconds (including the new request). 
* Specifically, return the number of requests that have happened in the inclusive range [t - 3000, t].

It is guaranteed that every call to ping uses a strictly larger value of t than the previous call.

## 解法1
1. 使用list存每次的time
2. 每次ping時將時間，加到列表尾部；再用for loop由尾部遍歷每個時間並計數，當超出範圍[t-3000,t] break。
```python3
class RecentCounter:
    
    def __init__(self):
        self.request_time = []
        
    def ping(self, t: int) -> int:
        self.request_time.append(t)
        count = 0
        start = t-3000
        for i in range(len(self.request_time)-1,-1,-1):
            if self.request_time[i] < start:
                break
            count += 1
        return count
```

## 解法2
1. 使用deque存每次的time。
2. 每次ping時將時間，加到deque尾部；再用while loop去除超出範圍[t-3000,t]的項目，當符合範圍時 break。
* deque的優點，在最前端刪除(popleft)、添加元素(appendleft)時，複雜度為O(1)
```python3
class RecentCounter:

    def __init__(self):
        from collections import deque
        self.request_time = deque()
        
    def ping(self, t: int) -> int:
        self.request_time.append(t)
        count = 0
        start = t-3000
        while self.request_time:
            if self.request_time[0] < start:
                self.request_time.popleft()
            else:
                break

        return len(self.request_time)
```


