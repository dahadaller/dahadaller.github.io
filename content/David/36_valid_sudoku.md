Title: 36 Valid Sudoku (David)
Date: 2020-06-09 17:00
Authors: David Hadaller
Tags: Week 2, LeetCode



Here we solve the [Valid Sudoku Problem](https://leetcode.com/problems/valid-sudoku/) from LeetCode.

> Determine if a 9x9 Sudoku board is valid. Only the filled cells need to be validated **according to the following rules**:
>
> 1. Each row must contain the digits `1-9` without repetition.
> 2. Each column must contain the digits `1-9` without repetition.
> 3. Each of the 9 `3x3` sub-boxes of the grid must contain the digits `1-9` without repetition.
>
> ![img](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)
>  A partially filled sudoku which is valid.
>
> The Sudoku board could be partially filled, where empty cells are filled with the character `'.'`.
>
> **Example 1:**
>
> ```
> Input:
> [
>   ["5","3",".",".","7",".",".",".","."],
>   ["6",".",".","1","9","5",".",".","."],
>   [".","9","8",".",".",".",".","6","."],
>   ["8",".",".",".","6",".",".",".","3"],
>   ["4",".",".","8",".","3",".",".","1"],
>   ["7",".",".",".","2",".",".",".","6"],
>   [".","6",".",".",".",".","2","8","."],
>   [".",".",".","4","1","9",".",".","5"],
>   [".",".",".",".","8",".",".","7","9"]
> ]
> Output: true
> ```
>
> **Example 2:**
>
> ```
> Input:
> [
>   ["8","3",".",".","7",".",".",".","."],
>   ["6",".",".","1","9","5",".",".","."],
>   [".","9","8",".",".",".",".","6","."],
>   ["8",".",".",".","6",".",".",".","3"],
>   ["4",".",".","8",".","3",".",".","1"],
>   ["7",".",".",".","2",".",".",".","6"],
>   [".","6",".",".",".",".","2","8","."],
>   [".",".",".","4","1","9",".",".","5"],
>   [".",".",".",".","8",".",".","7","9"]
> ]
> Output: false
> Explanation: Same as Example 1, except with the 5 in the top left corner being 
>     modified to 8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.
> ```
>
> **Note:**
>
> - A Sudoku board (partially filled) could be valid but is not necessarily solvable.
> - Only the filled cells need to be validated according to the mentioned rules.
> - The given board contain only digits `1-9` and the character `'.'`.
> - The given board size is always `9x9`.



This solution holds all data in a set called `big` instead of using separate data structures for the rows, columns and boxes. Rows that already have a given number are placed in `big` as `(row, cell)` tuples, where `cell` is the number the `row` already contains. Columns reverse the tuple order with `(cell, col)` tuples. And the boxes use integer division to find the value of the nearest upper-left-hand corner with `row//3` and `col//3` .  This means that the 3-tuple `(row//3, col//3, cell)` associates each number in `cell` with the closest upper-left-hand corner.

```python
class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        
        big = set()
        for row in range(0,9):
            for col in range(0,9):
                
                if board[row][col]!='.':
                    
                    cell = board[row][col]
                    
                    if (row, cell) in big or (cell,col) in big or (row//3,col//3,cell) in big:
                        return False
                    
                    big.add((row, cell))
                    big.add((cell,col))
                    big.add((row//3,col//3,cell))
        return True
                    
```





