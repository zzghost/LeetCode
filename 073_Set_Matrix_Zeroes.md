# Set Matrix Zeroes
## Description
Given a m x n matrix, if an element is 0, set its entire row and column to 0. Do it in place.  

Follow up:  
Did you use extra space?  
A straight forward solution using O(mn) space is probably a bad idea.  
A simple improvement uses O(m + n) space, but still not the best solution.  
Could you devise a constant space solution?  
## Solution
1. Use new array as mark.  
**Complexity: Time O(mn), Space O(1).**
```java
public void setZeroes(int[][] matrix) {
    if(matrix == null || matrix.length == 0)
        return ;

    int row = matrix.length, col = matrix[0].length;

    int[] markRow = new int[row];
    int[] markCol = new int[col];
    //Find zero.
    for(int i = 0; i < row; i++)
        for(int j = 0; j < col; j++)
            if(matrix[i][j] == 0){
                markRow[i] = 1;
                markCol[j] = 1;
            }
    //change to Zero.
    for(int i = 0; i < row; i++){
        if(markRow[i] == 1){
            for(int j = 0; j < col; j++)
                matrix[i][j] = 0;
        }
    }
    for(int j = 0; j < col; j++){
        if(markCol[j] == 1)
            for(int i = 0; i < row; i++)
                matrix[i][j] = 0;
    }
}
```
2. Use array as mark.  
Use `row=0` and `col=0` to mark.  
**Complexity: Time O(mn), Space O(1).**  
```java
public void setZeroes(int[][] matrix) {
    if(matrix == null || matrix.length == 0)
        return ;

    int row = matrix.length, col = matrix[0].length;
    boolean originRow = false, originCol = false;
    for(int i = 0; i < row; i++){
        for(int j = 0; j < col; j++){
            if(matrix[i][j] == 0){
                if(i == 0)
                    originCol = true;
                if(j == 0)
                    originRow = true;
                matrix[i][0] = 0;
                matrix[0][j] = 0;
            }
        }
    }

    for(int i = 1; i < matrix.length; i++)
        for(int j = 1; j < matrix[0].length; j++)
            if(matrix[i][0] == 0 || matrix[0][j] == 0) 
                matrix[i][j] = 0;

    if(originCol)
        for(int j = 0; j < col; j++)
            matrix[0][j] = 0;

    if(originRow)
        for(int i = 0; i < row; i++)
            matrix[i][0] = 0;

}
```
