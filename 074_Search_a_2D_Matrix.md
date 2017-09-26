# Search a 2D Matrix
## Description
Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

Integers in each row are sorted from left to right.
The first integer of each row is greater than the last integer of the previous row.
## Example
Consider the following matrix:
```
[
[1,   3,  5,  7],
[10, 11, 16, 20],
[23, 30, 34, 50]
]
Given target = 3, return true.
```
## Solution
**Complexity: Time O(m+n), Space O(1).**
```java
public boolean searchMatrix(int[][] matrix, int target) {
    if(matrix == null || matrix.length == 0)
        return false;

    int row = 0, col = matrix[0].length - 1;
    while(row < matrix.length && col >= 0){
        if(matrix[row][col] == target)
            return true;
        if(matrix[row][col] < target)
            row++;
        else
            col--;
    }
    return false;
}
```
