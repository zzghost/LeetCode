# Minimum Path Sum
## Description
Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path. 

**Note:** You can only move either down or right at any point in time.  
## Solution
Dynamic Programming.  
**Complexity: Time O(mn), Space O(n).**  
```java
public int minPathSum(int[][] grid) {
    int row = grid.length, col = grid[0].length;
    int[] dp = new int[col];
    dp[0] = grid[0][0];
    for(int i = 1; i < col; i++)
        dp[i] = dp[i-1] + grid[0][i];

    for(int i = 1; i < row; i++){
        dp[0] = dp[0] + grid[i][0];
        for(int j = 1; j < col; j++){
            dp[j] = Math.min(dp[j], dp[j - 1]) + grid[i][j];
        }
    }

    return dp[col - 1];
}
```
