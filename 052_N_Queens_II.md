# N-Queens II
Follow up for [N-Queens problem](https://github.com/zzghost/leetcode/blob/master/051_N_Queens.md).  

Now, instead outputting board configurations, return the total number of distinct solutions.  
## Solution
BackTracking.  
```java
class Solution {
    public int count = 0;
    public boolean isValid(char[][] board, int row, int col){
        int n = board.length;
        for(int i = 0; i < row; i++)
            for(int j = 0; j < n; j++)
                if(board[i][j] == 'Q' && (row + col == i + j || row + j == col + i || col == j))
                    return false;
        return true;
    }
    public void find(char[][] board, int n, int row){
        if(row == n){
            count++;
            return ;
        }
        if(row < n)
        for(int i = 0; i < n; i++){
            if(isValid(board, row, i)){
                board[row][i] = 'Q';
                find(board, n, row + 1);
                board[row][i] = '.';
            }
        }
    }
    public int totalNQueens(int n) {
        char[][] board = new char[n][n];
        for(int i = 0; i < n; i++)
            Arrays.fill(board[i], '.');
        find(board, n, 0);
        return count;
    }
}
```
