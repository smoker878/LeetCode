# [3016. Minimum Number of Pushes to Type Word II](https://leetcode.com/problems/minimum-number-of-pushes-to-type-word-ii/description/)

## 題目描述
* 你要根據字母出現的頻率，來設計一個手機鍵盤
* 這個鍵盤的數字鍵2~9可以放字母，按一下為第一個字母，兩下為第二個字母
* 你要根據題目給你的字串，設計這個鍵盤，並可以按最少的次數
  ![手機鍵盤](https://assets.leetcode.com/uploads/2023/12/26/keypaddesc.png)

## 解法1
* 因為有8個按鍵可以放字母，我們要將最常出現的放在第一順位(只要按一下就可以的)，其次第二順位......
* 我們先用字典紀錄每個字母出現的次數
* 用一個列表存，根據出現次數排序的字母
* 計算按的次數：用一個for loop遍歷根據出現次數排列的列表，每8次增加一次按的次數，把每次每個字母案的次數加起來
```python3
class Solution:
    def minimumPushes(self, word: str) -> int:
        count = {} #{字母:次數}
        for w in word:
            if w not in count:
                count[w] = 1
            else:
                count[w] += 1
        appear_rank =  sorted(count, key= lambda x: count[x], reverse = True) #根據次數排序
        # print(appear_rank)

        push_sum = 0
        push_time = 1
        c = 0
        for w in appear_rank:  #計算按的次數
            c += 1
            push_sum += push_time* count[w]
            # print(f"{w},{count[w]},{push_time},{c}")
            if c >= 8:
                push_time += 1
                c = 0
        return push_sum
    
   
```
