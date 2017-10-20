# Triangle
## Description
Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

For example, given the following triangle
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
The minimum path sum from top to bottom is 11 (i.e., 2 + 3 + 5 + 1 = 11).

**Note:**
Bonus point if you are able to do this using only O(n) extra space, where n is the total number of rows in the triangle.


## Solution
Dynamic Programming.  
1. From up to bottom.  
`dp[j] = min(dp[j-1], dp[j]) + array[j]`,but we should deal with the first and the last element in each level, which leads to the optimal solution.  
**Complexity: O(n^2), Space O(n).**
```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        int n = triangle.size();
        int[] dp = new int[n];
        int minPath = Integer.MAX_VALUE;
        //each level
        dp[0] = (int)triangle.get(0).toArray()[0];
        for(int i = 1; i < n; i++){
            Object[] array = triangle.get(i).toArray();
            dp[i] = dp[i - 1] + (int)array[i];
            for(int j = i - 1; j > 0; j--){
                dp[j] = Math.min(dp[j - 1], dp[j]) + (int)array[j];
            }
            dp[0] += (int)array[0];
        }
        for(int i = 0; i < n; i++)
            minPath = Math.min(minPath, dp[i]);
        return minPath;
    }
}
```
2. From bottom to up.
The code is more simple and elegant.We don't need to consider the boundary and `minLen`.     
```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        int n = triangle.size();
        int[] dp = new int[n + 1];
        for(int i = n - 1; i >= 0; i--){
            for(int j = 0; j <= i; j++)
                dp[j] = Math.min(dp[j], dp[j + 1]) + triangle.get(i).get(j);
        }
        return dp[0];
    }
}
```
