# Unique Paths II
## Description
Follow up for "Unique Paths":  

Now consider if some obstacles are added to the grids. How many unique paths would there be?  

An obstacle and empty space is marked as 1 and 0 respectively in the grid.  

For example,  
```
There is one obstacle in the middle of a 3x3 grid as illustrated below.

[
[0,0,0],
[0,1,0],
[0,0,0]
]
The total number of unique paths is 2.  
```
**Note:** m and n will be at most 100.  
## Solution
Dynamic Programming.  
**Complexity: Time O(mn), Space O(m).**
```java
public int uniquePathsWithObstacles(int[][] obstacleGrid) {
    if(obstacleGrid == null || obstacleGrid.length == 0)
        return 0;
    int n = obstacleGrid.length, m = obstacleGrid[0].length;
    int[] dp = new int[m];
    dp[0] = 1;
    for(int i = 0; i < n; i++)
        for(int j = 0; j < m; j++)
            if(obstacleGrid[i][j] == 1)
                dp[j] = 0;
            else if(j > 0)
                dp[j] += dp[j - 1];

    return dp[m - 1];
}
```
