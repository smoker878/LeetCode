# [36. Valid Sudoku](https://leetcode.com/problems/valid-sudoku/description/?envType=study-plan-v2&envId=top-interview-150)
# 題目描述
* 給你一個二微陣列，它是一個數獨
* 每行、每列、每個九宮格中不能有重複數字

# 解法
## 驗證列Row
* 由兩個for迴圈，外迴圈遍歷每列row，在外迴圈中放一個 set紀錄出現過的數字，內迴圈遍歷列中每個元素，若有出現重複數字，就代表這篇數獨不合規則。
## 驗證行Column
* 方法上同，只是將外迴圈改為遍歷column。

## 驗證行九宮格
* 這是這題比較難的部分，要由每個網格row和col的第一格開始遍歷。
* 由兩個for迴圈，找出每個網格的第一格(r, c)，並放一個set紀錄出現過的數字。並再用兩個for迴圈遍歷內部每一格(r+i, c+j)

| (0,0) | (0,3) | (0,6) |
| --- | --- | --- |
| (3,0) | (3,3) | (3,6) |
| (6,0) | (6,3) | (6,6) |

``` python3
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        for r in range(9):  #驗證row
            num_appear = set()
            for c in range(9):
                if board[r][c] not in num_appear:
                    num_appear.add(board[r][c])
                elif board[r][c].isdigit():
                    return False

        for c in range(9):  #驗證column
            num_appear = set()
            for r in range(9):
                if board[r][c] not in num_appear:
                    num_appear.add(board[r][c])
                elif board[r][c].isdigit():
                    return False

        for r in range(0,9,3):  #驗證grid
            for c in range(0,9,3):
                num_appear = set()
                for i in range(3):
                    for j in range(3):
                        if board[r+i][c+j] not in num_appear:
                            num_appear.add(board[r+i][c+j])
                        elif board[r+i][c+j].isdigit():
                            return False
        return True  
```
