# N-Queens
The n-queens puzzle is the problem of placing n queens on an n×n chessboard such that no two queens attack each other.  
Given an integer n, return all distinct solutions to the n-queens puzzle.

Each solution contains a distinct board configuration of the n-queens' placement, where 'Q' and '.' both indicate a queen and an empty space respectively.

For example,
There exist two distinct solutions to the 4-queens puzzle:
```
[
 [".Q..",  // Solution 1
  "...Q",
  "Q...",
  "..Q."],

 ["..Q.",  // Solution 2
  "Q...",
  "...Q",
  ".Q.."]
]
```
## Solution
BackTracking.  
```java
class Solution {
    List<List<String>> rst = new ArrayList<>();
    public boolean isValid(char[][] board, int row, int col){
        int n = board.length;
        for(int i = 0; i < row; i++)
            for(int j = 0; j < n; j++)
            //check three positions:45 degree, 135 degree and the column.
                if(board[i][j] == 'Q' && (row + col == i + j || row + j == col + i || col == j))
                    return false;
        return true;
    }
    public void find(char[][] board, int n, int row){
        if(row == n){
            List<String> aList = new ArrayList<>();
            for(int i = 0; i < n; i++)
                aList.add(String.valueOf(board[i]));
            rst.add(aList);
        }
        if(row < n){
            for(int i = 0; i < n; i++){
                if(isValid(board, row, i)){
                    board[row][i] = 'Q';
                    find(board, n, row + 1);
                    board[row][i] = '.';
                }
            }
        }
    }
    public List<List<String>> solveNQueens(int n) {
        char[][] board = new char[n][n];
        for(int i = 0; i < n; i++)
            Arrays.fill(board[i], '.');
        find(board, n, 0);
        return rst;
    }
}
```
