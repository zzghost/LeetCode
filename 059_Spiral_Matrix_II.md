# Spiral Matrix II
## Description
Given an integer n, generate a square matrix filled with elements from 1 to n2 in spiral order.  

For example,  
Given n = 3,  

You should return the following matrix:  
```
[
[ 1, 2, 3 ],
[ 8, 9, 4 ],
[ 7, 6, 5 ]
]
```
## Solution
**Complexity: Time O(n^2), Space O(n^2).**
```java
public int[][] generateMatrix(int n) {
    int[][] matrix = new int[n][n];

    int count = 1;
    int left = 0, right = n - 1;
    int top = 0, bottom = n - 1;
    while(left <= right){
        for(int j = left; j <= right; j++)
            matrix[top][j] = count++;
        top++;

        for(int i = top; i <= bottom; i++)
            matrix[i][right] = count++;
        right--;

        for(int j = right; j >= left; j--)
            matrix[bottom][j] = count++;
        bottom--;

        for(int i = bottom; i >= top; i--)
            matrix[i][left] = count++;
        left++;
    }

    return matrix;
}
```
