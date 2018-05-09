# Surrounded Regions
## Description
Given a 2D board containing 'X' and 'O' (the letter O), capture all regions surrounded by 'X'.

A region is captured by flipping all 'O's into 'X's in that surrounded region.

Example:
```
X X X X
X O O X
X X O X
X O X X
```
After running your function, the board should be:
```
X X X X
X X X X
X X X X
X O X X
```
**Explanation:**  

Surrounded regions shouldn’t be on the border, which means that any 'O' on the border of the board are not flipped to 'X'. Any 'O' that is not on the border and it is not connected to an 'O' on the border will be flipped to 'X'. Two cells are connected if they are adjacent cells connected horizontally or vertically.

## Solution
1. Depth-First Search.  
If we do dfs on 'O' point by point, it turns out "Runtime Error:stack overflow".  
Do dfs operation on the boarder 'O', the 'O' traversed will be replaced by 'W'.  
After that, replace the remained 'O' to 'X' and 'W' to 'O'.  
```java
class Solution {
    public void dfs(char[][] board, int row, int col){
        if(row < 0 || row >= board.length || col < 0 || col >= board[0].length){
            return ;
        }
        if(board[row][col] == 'O'){
            board[row][col] = 'W';
            dfs(board, row - 1, col);
            dfs(board, row + 1, col);
            dfs(board, row, col - 1);
            dfs(board, row, col + 1);
        }
    }
    public void solve(char[][] board) {
        if(board == null || board.length == 0){
            return ;
        }
        int m = board.length, n = board[0].length;
        for(int i = 0; i < m; i++){
            if(board[i][0] == 'O'){
                dfs(board, i, 0);
            }
            if(board[i][n - 1] == 'O'){
                dfs(board, i, n - 1);
            }
        }
        for(int i = 0; i < n; i++){
            if(board[0][i] == 'O'){
                dfs(board, 0, i);
            }
            if(board[m - 1][i] == 'O'){
                dfs(board, m - 1, i);
            }
        }
        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                if(board[i][j] == 'O'){
                    board[i][j] = 'X';
                }
                if(board[i][j] == 'W'){
                    board[i][j] = 'O';
                }
            }
        }
    }
}
```
2. Breadth-First Search.  
```java
class Solution {
    class Position{
        int x, y;
        Position(int x, int y){
            this.x = x;
            this.y = y;
        }
    }
    public void solve(char[][] board) {
        if(board == null || board.length == 0){
            return ;
        }
        int m = board.length, n = board[0].length;
        Queue<Position> queue = new LinkedList<>();
        for(int i = 0; i < m; i++){
            if(board[i][0] == 'O'){
                queue.offer(new Position(i, 0));
            }
            if(board[i][n - 1] == 'O'){
                queue.offer(new Position(i, n - 1));
            }
        }
        for(int i = 0; i < n; i++){
            if(board[0][i] == 'O'){
                queue.offer(new Position(0, i));
            }
            if(board[m - 1][i] == 'O'){
                queue.offer(new Position(m - 1, i));
            }
        }
        final int[] dx = {-1, 0, 0, 1};
        final int[] dy = {0, 1, -1, 0};
        while(!queue.isEmpty()){
            Position top = queue.poll();
            board[top.x][top.y] = 'W';
            for(int i = 0; i < dx.length; i++){
                int newX = top.x + dx[i], newY = top.y + dy[i];
                if(newX >= 0 && newY >= 0 && newX < m && newY < n){
                    if(board[newX][newY] == 'O'){
                        queue.offer(new Position(newX, newY));
                    }
                }
            }
        }
        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                if(board[i][j] == 'O'){
                    board[i][j] = 'X';
                }
                if(board[i][j] == 'W'){
                    board[i][j] = 'O';
                }
            }
        }
    }
}
```
3. Union-Find.  
Let the point be 1-D array and do the union operation.Each time we just consider the right and down point.      
Let the larger point be the root.  
Take below array as an example.  
```
O X X X X
X O X O X
X X X O X
O X O O O
```
The root array is:
```
0 5 1 1 1
5 6 1 17 1
5 5 1 8 1
15 5 17 8 17
```
point `17` and `18`: because `18` has been updated by point `13`, and its root is `8`.  When union(17, 18), it's actually union `17` and `8`.  
```java
class Solution {
    public int find(int x, int[] root){
        int r = x;
        while(r != root[r]){
            r = root[r];
        }
        return r;
    }
    public void union(int x, int y, int[] root, boolean[] isEdge){
        int rootX = find(x, root), rootY = find(y, root);
        if(rootX != rootY){
          //key steps are here:
            root[rootY] = rootX;
            if(isEdge[rootY]){
                isEdge[rootX] = true;
            }
        }
    }
    public void solve(char[][] board) {
        if(board == null || board.length == 0){
            return ;
        }
        int m = board.length, n = board[0].length;
        int[] root = new int[m * n];
        boolean[] isEdge = new boolean[m * n];
        for(int i = 0; i < m * n; i++){
            root[i] = i;
            int x = i / n, y = i % n;
            if(x == 0 || x == m - 1 || y == 0 || y == n - 1){
                if(board[x][y] == 'O'){
                    isEdge[i] = true;
                }
            }
        }

        for(int i = 0; i < m * n; i++){
            int x = i / n, y = i % n;
            int down = x + 1, right = y + 1;
            if(down < m && board[x][y] == board[down][y]){
                union(i, i + n, root, isEdge);
            }
            if(right < n && board[x][y] == board[x][right]){
                union(i, i + 1, root, isEdge);
            }
        }
        for(int i = 0; i < m * n; i++){
            int x = i / n, y = i % n;
            if(board[x][y] == 'O' && !isEdge[find(i, root)]){
                board[x][y] = 'X';
            }
        }
    }
}
```
