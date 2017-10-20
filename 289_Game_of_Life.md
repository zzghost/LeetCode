
# Game of Life
## Description
According to the [Wikipedia's article](https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life): "The Game of Life, also known simply as Life, is a cellular automaton devised by the British mathematician John Horton Conway in 1970."

Given a board with m by n cells, each cell has an initial state live (1) or dead (0). Each cell interacts with its eight neighbors (horizontal, vertical, diagonal) using the following four rules (taken from the above Wikipedia article):

Any live cell with fewer than two live neighbors dies, as if caused by under-population.
1. Any live cell with two or three live neighbors lives on to the next generation.
2. Any live cell with more than three live neighbors dies, as if by over-population..
3. Any dead cell with exactly three live neighbors becomes a live cell, as if by reproduction.
4. Write a function to compute the next state (after one update) of the board given its current state.

**Follow up: **
1. Could you solve it in-place? Remember that the board needs to be updated at the same time: You cannot update some cells first and then use their updated values to update other cells.
2. In this question, we represent the board using a 2D array. In principle, the board is infinite, which would cause problems when the active area encroaches the border of the array. How would you address these problems?

## Solution
Bit manipulation.  
Use two bits to represent the state:  
1st is the next state  
2nd is the current state  
Thus:  
`00` : dead <- dead  
`10` : alive <- dead  
`01` : dead <- alive  
`11` : alive <- alive  
Procedure:  
1. count each neighbors.  
2. change the state, if `countAlive >= 2 && countALive <= 3 && currentState == 1`, state becomes `11` = 3. if`countAlive == 3 && currentState == 3`, state becomds `10`= 2. Other 2 states can be neglect cos they don't change.  
3. Right shift the bits.  
**Complexity: Time O(n^2), Space O(1).**
```java
class Solution {
    public int liveNeighbors(int[][] board, int i, int j, int m, int n){
        int lives = 0;
        for(int x = Math.max(i - 1, 0); x <= Math.min(i + 1, m - 1); x++)
            for(int y = Math.max(j - 1, 0); y <= Math.min(j + 1, n - 1); y++)
                lives += board[x][y] & 1;
        lives -= board[i][j] & 1;
        return lives;
    }
    public void gameOfLife(int[][] board) {
        int m = board.length, n = board[0].length;
        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                int countAlive = liveNeighbors(board, i, j, m, n);
                if(board[i][j] == 1 && (countAlive >= 2 && countAlive <= 3))
                    board[i][j] = 3;
                if(board[i][j] == 0 && countAlive == 3)
                    board[i][j] = 2;
            }
        }
        for(int i = 0; i < m; i++)
            for(int j = 0; j < n; j++)
                board[i][j] >>= 1;
    }
}
```
