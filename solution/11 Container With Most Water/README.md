# [11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/description/)

## 題目描述
* height為一個列表，每個值height[i]表示牆高度，i 之間的距離表示寬度。
* 尋找height[i],height[j]，所為起來的容器，所能儲存的最大水量

![圖](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)
## 解法
1. 讓l, r 為指針，指向最左(index=0)和最右(index=len(len(height)-1))兩端。
1. 裝水量為兩端矮的那端為高，兩端距離相減為寬。
1. 判斷兩端，找矮的那端往中間移，當一到比之前自己高或比另一端高，停下
1. 每次停下判斷一次容量是否比之前大

```python3
class Solution:
    def maxArea(self, height: List[int]) -> int:
        l = 0  
        r = len(height)-1
        max_cont = (r-l)*min(height[l], height[r]) #判斷容量
        while l < r: #r和l相遇結束

            if height[l] < height[r] : #l為矮的那端
                last_height_l = height[l]
                while height[l] < height[r]:
                    l += 1           #l右移，遇到比r高或比之前自己高，停下
                    if height[l] >last_height_l:
                        break
                
            elif height[l] > height[r] : #r為矮的那端
                last_height_r = height[r]
                while height[l] > height[r]:
                    r -= 1   #r左移，遇到比l高或比之前自己高，停下
                    if height[r] >last_height_r:
                        break

            else:  #這邊為兩個相等的狀況，讓l右移(或讓r左移也可以)
                l += 1
            if (cont := (r-l)*min(height[l], height[r])) > max_cont:
                max_cont = cont
        return max_cont



            
   
```
