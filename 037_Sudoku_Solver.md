# Sudoku Solver
Write a program to solve a Sudoku puzzle by filling the empty cells.  

Empty cells are indicated by the character '.'.  

You may assume that there will be only one unique solution.  

## Solution
```java
class Solution {
    public boolean isValid(char[][] board, int row, int col, char t){
        int r = 3 * (row / 3), c = 3 * (col / 3);
        for(int i = 0; i < board.length; i++)
            if(board[row][i] == t || board[i][col] == t || board[r + i / 3][c + i % 3] == t)
                return false;

        return true;
    }
    public boolean solve(char[][] board){
        for(int i = 0; i < board.length; i++){
            for(int j = 0; j < board[0].length; j++){
                if(board[i][j] == '.'){
                    for(char c = '1'; c <= '9'; c++){
                        if(isValid(board, i, j, c)){
                            board[i][j] = c;
                            if(solve(board))
                                return true;
                            else
                                board[i][j] = '.';
                        }
                    }
                    return false;
                }
            }
        }
        return true;
    }
    public void solveSudoku(char[][] board) {
        if(board == null || board.length == 0)
            return ;
        solve(board);
    }
}
```
