# Valid Sudoku
Determine if a Sudoku is valid, according to: [Sudoku Puzzles - The Rules](http://sudoku.com.au/TheRules.aspx).

The Sudoku board could be partially filled, where empty cells are filled with the character '.'.


A partially filled sudoku which is valid.

Note:
A valid Sudoku board (partially filled) is not necessarily solvable. Only the filled cells need to be validated.

## Solution
Check rows, columns, grids one by one.  
```java
class Solution {
    public boolean isValidSudoku(char[][] board) {
        if(board == null || board.length == 0)
            return false;
        int n = board.length, m = board[0].length;
        if(m != n)
            return false;
        Map<Character, Integer> map = new HashMap<>();//<number, row i>
        //check row
        for(int row = 0; row < n; row++){
            map = new HashMap<>();
            for(int column = 0; column < n; column++){
                if(map.containsKey(board[row][column])){
                    return false;
                }
                else if(board[row][column] >= '1' && board[row][column] <= '9'){
                    map.put(board[row][column], row);
                }
                else if(board[row][column] == '.')
                    continue;
                else
                    return false;
            }
        }
        //check column
        for(int column = 0; column < n; column++){
            map = new HashMap<>();
            for(int row = 0; row < n; row++){
                if(board[row][column] == '.')
                    continue;
                if(map.containsKey(board[row][column])){
                    return false;
                }
                if(board[row][column] >= '1' && board[row][column] <= '9'){
                    map.put(board[row][column], row);
                }
            }
        }
        //check grid
        for(int row = 0; row <= 6; row = row + 3){
            for(int column = 0; column <= 6; column = column + 3){
                map = new HashMap<>();
                //check each grid
                for(int i = row; i < row + 3; i++){
                    for(int j = column; j < column + 3; j++){
                        if(board[i][j] == '.')
                            continue;
                        if(map.containsKey(board[i][j]))
                            return false;
                        else
                            map.put(board[i][j], i);
                    }
                }
            }
        }
        return true;
    }
}
```
A more concise solution:  
```java
class Solution {
    public boolean isValidSudoku(char[][] board) {
        for(int i = 0; i < 9; i++){
            HashSet<Character> rows = new HashSet<>();
            HashSet<Character> columns = new HashSet<>();
            HashSet<Character> grids = new HashSet<>();
            for(int j = 0; j < 9; j++){
                int columnIdx = (i % 3) * 3+ j % 3;
                int rowIdx = (i / 3) * 3 +  j / 3;
                if(board[i][j] != '.' && !rows.add(board[i][j]))
                    return false;
                if(board[j][i] != '.' && !columns.add(board[j][i]))
                    return false;
                if(board[rowIdx][columnIdx] != '.' && !grids.add(board[rowIdx][columnIdx]))
                    return false;
            }
        }
        return true;
    }
}
```
