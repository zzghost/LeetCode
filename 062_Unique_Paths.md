#Unique Paths
## Description
A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).  

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).  

How many possible unique paths are there?  

## Solution
1. Recursive.[Time Limit Exceeded]
```java
public int walk(int i, int j, int m, int n){
    if(i == m && j == n)
        return 1;
    if(i > m || j > n)
        return 0;
    return walk(i + 1, j, m, n) + walk(i, j + 1, m, n);

}
public int uniquePaths(int m, int n) {
    return walk(1, 1, m, n);
}
```
2. Dynamic Programming.  
Let `paths[i][j]` be the unique ways to position(i, j).  
`paths[i][j] = paths[i-1][j] + paths[i][j-1]`.  
Because `paths[i][j]` depends only on the left state and the up state, we minus space complexity from O(mn) to O(n).  
**Complexity: Time O(mn), Space O(n).**  
```java
public int uniquePaths(int m, int n) {
    int[] paths = new int[n];
    for(int i = 0; i < m; i++){
        paths[0] = 1;
        for(int j = 1; j < n; j++){
            paths[j] += paths[j - 1];
        }
    }
    return paths[n - 1];
}
```
