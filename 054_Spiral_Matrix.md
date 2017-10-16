# Spiral Matrix
## Description
Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

For example,
Given the following matrix:
```
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
```
You should return `[1,2,3,6,9,8,7,4,5]`.

## Solution
Just view it as a rectanguler and then deal with each edge.  
Must be careful with the bounds checking and the special case like n = 1 or m = 1.  
**Complexity: Time O(n^2), Space O(1).**
```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> sequence = new ArrayList<>();
        if(matrix == null || matrix.length == 0)
            return sequence;

        int m = matrix.length, n = matrix[0].length;
        int min = Math.min(m, n);
        for(int i = 0; i <= (min - 1) / 2; i++){
            //first[i][not fixed]
            for(int j = i; j < n - i; j++){
                sequence.add(matrix[i][j]);
            }
            //second,[not fixed][n - i - 1]
            for(int j = i + 1; j < m - i; j++)
                sequence.add(matrix[j][n - i - 1]);
            //third,[m - i - 1][not fixed]
            for(int j = n - i - 2; j >= i && m - i - 1 != i; j--)
                sequence.add(matrix[m - i - 1][j]);
            //fourth,[not fixed][i]
            for(int j = m - i - 2; j > i && n - i - 1 != i; j--)
                sequence.add(matrix[j][i]);
        }
        return sequence;
    }
}
```
