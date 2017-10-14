# Max Area of Island
## Description
Given a non-empty 2D array grid of 0's and 1's, an island is a group of 1's (representing land) connected 4-directionally (horizontal or vertical.)  
You may assume all four edges of the grid are surrounded by water.  

Find the maximum area of an island in the given 2D array. (If there is no island, the maximum area is 0.)  

Example 1:  
```
[[0,0,1,0,0,0,0,1,0,0,0,0,0],
[0,0,0,0,0,0,0,1,1,1,0,0,0],
[0,1,1,0,1,0,0,0,0,0,0,0,0],
[0,1,0,0,1,1,0,0,1,0,1,0,0],
[0,1,0,0,1,1,0,0,1,1,1,0,0],
[0,0,0,0,0,0,0,0,0,0,1,0,0],
[0,0,0,0,0,0,0,1,1,1,0,0,0],
[0,0,0,0,0,0,0,1,1,0,0,0,0]]
Given the above grid, return 6. Note the answer is not 11, because the island must be connected 4-directionally.  
```
Example 2:  
```
[[0,0,0,0,0,0,0,0]]
Given the above grid, return 0.
```
**Note:** The length of each dimension in the given grid does not exceed 50.  
## Solution
Backtracking.
**Complexity: Time (mn4^mn), Space O(mn).**
```java
public int count(int[][] grid, int row, int col){
    int r = grid.length, c = grid[0].length;
    if(row >= r || row < 0 || col >= c || col < 0)
        return 0;
    if(grid[row][col] == 0)
        return 0;
    grid[row][col] = 0;
    return 1 + count(grid, row - 1, col) + count(grid, row + 1, col) + count(grid, row, col - 1) + count(grid, row, col + 1);

}
public int maxAreaOfIsland(int[][] grid) {
    int r = grid.length, c = grid[0].length;
    int rst = 0;
    for(int i = 0; i < r; i++)
        for(int j = 0; j < c; j++){
            if(grid[i][j] == 1)
                rst = Math.max(rst, count(grid, i, j));
        }
    return rst;
}
```
