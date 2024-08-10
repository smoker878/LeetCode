# [128. Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/description/)

## 題目描述
* 給你一串為排序的數字，找出裡面[連號次數最多的]，返回連號次數

## 解法
* 先將nums轉成set，因為set找裡面的數字複雜度為O(1)。
* 隨機找一個數字做起點，然後先向後找，找不到了，再向前找。(每次有找到東西就remove掉，所以不會再重複出現在start)
* 每找完一輪就比較長度，看是否比之前的長
```python3
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        longest = 0

        nums = set(nums)

        while nums:  #空了就跳出
            count = 1
            start = nums.pop()  #起點

            cur = start+1
            while cur in nums: #向後找
                count += 1
                nums.remove(cur)
                cur += 1
            cur = start-1
            while cur in nums:  #向前找
                count += 1
                nums.remove(cur)
                cur -= 1

            if count >longest: #看連號次數是否比之前長
                longest = count
        return longest   
```
