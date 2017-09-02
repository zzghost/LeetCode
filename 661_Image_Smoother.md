# Image Smoother  
## Description  
Given a 2D integer matrix M representing the gray scale of an image, you need to design a smoother to make the gray scale of each cell becomes the average gray scale (rounding down) of all the 8 surrounding cells and itself. If a cell has less than 8 surrounding cells, then use as many as you can.  
**Note:**  
1. The value in the given matrix is in the range of [0, 255].  
2. The length and width of the given matrix are in the range of [1, 150].  
## Example  
```
Input:  
[[1,1,1],  
 [1,0,1],  
 [1,1,1]]  
Output:  
[[0, 0, 0],  
 [0, 0, 0],  
 [0, 0, 0]]  
Explanation:  
For the point (0,0), (0,2), (2,0), (2,2): floor(3/4) = floor(0.75) = 0  
For the point (0,1), (1,0), (1,2), (2,1): floor(5/6) = floor(0.83333333) = 0  
For the point (1,1): floor(8/9) = floor(0.88888889) = 0  
```
## Solution  
Brute Force.  
Complexity: Time O(n^2), Space O(1)  
```java
public int[][] imageSmoother(int[][] M) {
    int row = M.length, col = M[0].length;
    int[][] rst = new int[row][col];
    for(int i = 0; i < row; i++){
        for(int j = 0; j < col; j++){
            int sum = 0, count = 0;
            for(int m = -1; m <= 1; m++){
                if(i + m >= 0 && i + m < row){
                    for(int n = -1; n <= 1; n++){
                        if(j + n >= 0 && j + n < col){
                            sum++;
                            count+= M[i+m][j+n];
                        }
                    }
                } 
            }
            rst[i][j] = count / sum;
        }
    }
    return rst;
}
```
