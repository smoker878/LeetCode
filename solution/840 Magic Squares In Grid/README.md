# [840. Magic Squares In Grid](https://leetcode.com/problems/magic-squares-in-grid/description/)

## 題目描述
* 給你一個二維的列表
* 你要計算這個列表中包含幾個magic_square
* magic_square定義：row加總 == 15，column加總 == 15, 斜線加總 ==15;且只能包含數字1~9

## 解法
* 定義 一個is_magic_square函數，只要給它九宮格原點的座標，它會遍歷這個九宮格看是否符合 magic_square的條件。
  * 這個函數用兩個for Loop，它可以判斷row和column加總是否等於15，知道是否有重複數字，和是否有出現0
  * 斜線因為只有兩條，所以我直接把每個可能只接打出來驗證
  * 用這個函數要確保部會越界，要確保在< len(row)-2，< len(col)-2的範圍用
* 因為len(row) < 3，len(col) < 3 無法形成magic_square，所以可以直接返回 0
```python3
class Solution:
    def numMagicSquaresInside(self, grid: List[List[int]]) -> int:
        def is_magic_square(r,c):
            for i in range(3):
                row_sum = 0  #驗證_row
                col_sum = 0  #驗證_col
                appear = set()  #驗證_不重複
                for j in range(3):
                    if grid[r+i][c+j] == 0: #驗證是否出現0
                        return False
                    row_sum += grid[r+i][c+j]
                    col_sum += grid[r+j][c+i]
                    if grid[i+r][j+c] not in appear:
                        appear.add(grid[i+r][j+c])
                    else:
                        return False
                if row_sum != 15 or col_sum != 15: 
                    return False

            #驗證_斜線
            left_slash = grid[r][c] + grid[r+1][c+1] + grid[r+2][c+2]
            right_slash = grid[r][c+2] + grid[r+1][c+1] + grid[r+2][c]
            if left_slash != 15 or right_slash != 15:
                return False
            return True

        if len(grid) < 3 or len(grid[0]) < 3: # <3 無法形成magic_square
            return 0

        res = 0
        for i in range(len(grid)-2):
            for j in range(len(grid)-2):
                if is_magic_square(i, j):
                    res += 1
        return res          
```
