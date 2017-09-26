# Word Search
## Description
Given a 2D board and a word, find if the word exists in the grid.  

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.  

## Example
```
Given board =

[
['A','B','C','E'],
['S','F','C','S'],
['A','D','E','E']
]
word = "ABCCED", -> returns true,
word = "SEE", -> returns true,
word = "ABCB", -> returns false.
```
## Solution
Recursive.  
**Complexity: Time O(mn4^k), Space O(mn).k is `word`'s length.**
```java
public boolean find(char[][] board, int r, int c, char[] alpha, int idx){
    if(idx == alpha.length)
        return true;
    if(r >= board.length || r < 0 || c < 0 || c >= board[0].length || alpha[idx] != board[r][c])
        return false;
    char tmp = board[r][c];
    board[r][c] = '0';
    boolean exist = find(board, r + 1 , c, alpha, idx + 1)
        || find(board, r - 1, c, alpha, idx + 1)
        || find(board, r, c + 1, alpha, idx + 1)
        || find(board, r, c - 1, alpha, idx + 1);
    board[r][c] = tmp;
    return exist;
}
public boolean exist(char[][] board, String word) {
    char[] alpha = word.toCharArray();
    if(board == null || board.length == 0 || board.length * board[0].length < word.length())
        return false;
    int row = board.length, col = board[0].length;
    for(int i = 0; i < row; i++)
        for(int j = 0; j < col; j++){
            if(find(board, i, j, alpha, 0))
                return true;
        }
    return false;
}
```
