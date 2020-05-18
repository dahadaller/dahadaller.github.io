Title: 200 Number of Islands (Kieran)
Date: 2020-05-18
Authors: Kieran Duggan
Tags: LeetCode, Bloomberg

>Given a 2d grid map of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

```python
class Solution:
    grid = list()
    
    def dfs(self,x,y):
        if self.grid[x][y] == '0':
            return
        self.grid[x][y] = '0'
        
        if x-1>=0:
            self.dfs(x-1,y)
        
        if x+1 < len(self.grid):
            self.dfs(x+1,y)
        
        if y-1>=0:
            self.dfs(x,y-1)
        
        if y+1 < len(self.grid[x]):
            self.dfs(x,y+1)
            
        
    def numIslands(self, local_grid: List[List[str]]) -> int:
        self.grid = local_grid
        count = 0
        for i in range(0,len(self.grid)):
            for j in range(0,len(self.grid[i])):
                if self.grid[i][j] == '1':
                    count+=1
                    #print(f'{self.grid[0]}\n{self.grid[1]}\n{self.grid[2]}\n{self.grid[3]}\n')
                    self.dfs(i,j)
                    
        return count
```
