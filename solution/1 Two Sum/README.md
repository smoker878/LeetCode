# [1. Two Sum](https://leetcode.com/problems/two-sum/description/)

## 題目描述
* Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.
* nums是一個數組，尋找裡面的整數兩個相加為target。
* 返回這兩個數的index

## 解法
* 用一個for循環遍歷nums，用一個字典(appear)存出現過的數字和它的index
* other_num為每個數字和target的差
* 只要other_num有出現在appear裡代表就是尋找到了
```python3
class RecentCounter:
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        appear = {nums[0]:0}  #{num:loc}
        for i in range(1,len(nums)):
            other_num = target - nums[i]
            if other_num in appear:
                return [appear[other_num],i]
            
            if nums[i] not in appear:
                appear[nums[i]] = i    
   
```


## 笨解法
這是我寫的第一題LeetCode，那時候我對演算法完全不了解，我就用兩個for loop來遍歷nums，把一個複雜度O(n)用O(n^2)來完成。
![](./img.png)
```python3
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        lenNum =len(nums)
        for i in range(lenNum):
            for j in range(i+1,lenNum):
                if nums[i] + nums[j] == target:
                    return [i,j]
                    break
```