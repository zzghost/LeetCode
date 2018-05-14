# Maximal Square
## Description
Given a 2D binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.

Example:
```
Input:

1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0

Output: 4
```
## Solution
Dynamic Programming.  
```java
class Solution {
    public int maximalSquare(char[][] matrix) {
        if(matrix == null || matrix.length == 0){
            return 0;
        }
        int m = matrix.length, n = matrix[0].length;
        int rst = 0;
        int[][] dp = new int[m][n];
        for(int i = 0; i < m; i++){
            if(matrix[i][0] == '1'){
                rst = 1;
                dp[i][0] = 1;
            }
        }
        for(int j = 0; j < n; j++){
            if(matrix[0][j] == '1'){
                rst = 1;
                dp[0][j] = 1;
            }
        }
        for(int i = 1; i < m; i++){
            for(int j = 1; j < n; j++){
                if(matrix[i][j] == '1'){
                    dp[i][j] = Math.min(dp[i - 1][j - 1], Math.min(dp[i - 1][j], dp[i][j - 1])) + 1;
                }
                rst = Math.max(rst, dp[i][j]);
            }
        }
        return rst * rst;
    }
}
```
