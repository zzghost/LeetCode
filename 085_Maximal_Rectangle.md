# Maximal Rectangle
## Description
Given a 2D binary matrix filled with 0's and 1's, find the largest rectangle containing only 1's and return its area.

For example, given the following matrix:
```
1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0
```
Return 6.
## Solution
There's an Chinese blog article which states very clear.[Click](https://www.cnblogs.com/lupx/archive/2015/10/20/leetcode-85.html).
1. Dynamic Programming  
leftBound:Overall left bound(the first `1`'s position) of all rows.  
rightBound:Overall right bound(the first `0`'s position) of all rows.  
int[] left:from `0` to `j`,the first `1`'s position  
int[] right: from `j` to the end of the row, the first `0`'s position  
int[] height: the cumulative height.Update to `0` when it meets `0` at this position.  
Position(i,j)'s max area can be calculated by `height[i] * (right[i] - left[i])`  
**Complexity: Time O(mn), Space O(n)**
```java
class Solution {
    public int maximalRectangle(char[][] matrix) {
        if(matrix == null || matrix.length == 0)
            return 0;
        int m = matrix.length, n = matrix[0].length;
        int[] left = new int[n];
        int[] right = new int[n];
        int[] height = new int[n];
        int maxArea = 0;
        //Initialize the array first.
        Arrays.fill(right, n);
        for(int i = 0; i < m; i++){ //each row
            int leftBound = 0, rightBound = n;
            //update left array
            for(int j = 0; j < n; j++){
                if(matrix[i][j] == '0'){
                    leftBound = j + 1;
                    left[j] = 0;
                }
                else
                    left[j] = Math.max(leftBound, left[j]);
            }
            //update right array
            for(int j = n - 1; j >= 0; j--){
                if(matrix[i][j] == '0'){
                    rightBound = j;
                    right[j] = n;
                }
                else
                    right[j] = Math.min(rightBound, right[j]);
            }
            //update height array
            for(int j = 0; j < n; j++){
                height[j] = (matrix[i][j] == '0') ? 0 : (height[j] + 1);
            }
            //calculate the area
            for(int j = 0; j < n; j++)
                maxArea = Math.max(maxArea, (right[j] - left[j]) * height[j]);
        }
        return maxArea;
    }
}
```
2. View it as [084. Largest Rectangle in Histogram](https://github.com/zzghost/leetcode/blob/master/084_Largest_Rectangle_in_Histogram.md)  
If the matrix has only one row, like `[1,0,1,1,1,0,0,1,1,1,1]`, we may consider it as width = 1, height=1 bars.And we use No.84's algorithm like Stack and get the answer = 4.  
Then, if there's 2 rows, like:
```
1 0 1 1 1 0 0 1 1 1 1
0 1 0 0 1 1 1 1 1 1 1
```
We can update the height array from `[1,0,1,1,1,0,0,1,1,1,1]` to `[0,1,0,0,2,1,1,2,2,2,2]` and then use 084's algorithm.  
**Complexity: Time O(mn), Space O(n).**
```java
class Solution {
    public int findMaxArea(int[] hist){
        //use leetcode No.84's algorithm
        Stack<Integer> stack = new Stack<>();
        int n = hist.length, maxArea = 0, h = hist[0];
        for(int i = 0; i <= n; i++){
            h = (i == n) ? 0 : hist[i];
            if(stack.isEmpty() || h >= hist[stack.peek()])
                stack.push(i);
            else{
                int tp = stack.pop();
                maxArea = Math.max(maxArea, (stack.isEmpty() ? i : (i - 1 - stack.peek())) * hist[tp]);
                i--;   
            }
        }
        return maxArea;
    }
    public int maximalRectangle(char[][] matrix) {
        if(matrix == null || matrix.length == 0)
            return 0;
        int m = matrix.length, n = matrix[0].length;
        int[] height = new int[n];
        int maxArea = 0;
        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++)
            //update the height.
                height[j] = (matrix[i][j] == '0') ? 0 : (height[j] + matrix[i][j] - '0');
            int tmpMaxArea = findMaxArea(height);
            maxArea = Math.max(tmpMaxArea, maxArea);
        }
        return maxArea;
    }
}
```
