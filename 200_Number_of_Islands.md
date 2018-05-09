# Number of Islands
## Description
Given a 2d grid map of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

Example 1:
```
Input:
11110
11010
11000
00000

Output: 1
```
Example 2:
```
Input:
11000
11000
00100
00011

Output: 3
```
## Solution
1. Depth-First Search  
```java
class Solution {
    public void bfs(char[][] grid, int row, int col, int[][] mark){
        if(row >= grid.length || row < 0 || col < 0 || col >= grid[0].length){
            return ;
        }
        if(grid[row][col] == '1' && mark[row][col] == 0){
            mark[row][col] = 1;
            bfs(grid, row - 1, col, mark);
            bfs(grid, row + 1, col, mark);
            bfs(grid, row, col - 1, mark);
            bfs(grid, row, col + 1, mark);
        }
    }
    public int numIslands(char[][] grid) {
        int islands = 0;
        if(grid == null || grid.length == 0){
            return islands;
        }
        int m = grid.length, n = grid[0].length;
        int[][] mark = new int[m][n];
        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                if(grid[i][j] == '1' && mark[i][j] == 0){
                    bfs(grid, i, j, mark);
                    islands++;
                }
            }
        }
        return islands;
    }
}
```
2. Breadth-First Search
```java
class Solution {
    class position{
        int x, y;
        position(int x, int y){
            this.x = x;
            this.y = y;
        }
    }
    public void bfs(char[][] grid, int[][] mark, Queue<position> queue){
        int[] dx = {-1, 0, 1, 0};
        int[] dy = {0, 1, 0, -1};
        while(!queue.isEmpty()){
            position top = queue.poll();
            for(int i = 0; i < dx.length; i++){
                int newX = top.x + dx[i], newY = top.y + dy[i];
                if(newX < 0 || newX >= grid.length || newY < 0 || newY >= grid[0].length){
                     continue;
                }
                if(grid[newX][newY] == '1' && mark[newX][newY] == 0){
                    mark[newX][newY] = 1;
                    queue.offer(new position(newX, newY));
                }
            }
        }
    }
    public int numIslands(char[][] grid) {
        if(grid == null || grid.length == 0){
            return 0;
        }
        int islands = 0;
        int[][] mark = new int[grid.length][grid[0].length];
        Queue<position> queue = new LinkedList<>();
        for(int i = 0; i < grid.length; i++){
            for(int j = 0; j < grid[0].length; j++){
                if(grid[i][j] == '1' && mark[i][j] == 0){
                    queue.offer(new position(i, j));
                    bfs(grid, mark, queue);
                    islands++;
                }
            }
        }
        return islands;
    }
}
```
3. Union-Find  
`count` is the initial numbers of islands.  
Each union operation is like building an edge between two islands.So after uinion, the number of islands is decremented by 1.  
```java
class Solution {
    int count = 0;
    public int find(int x, int[] root){
        int r = x;
        while(r != root[r]){
            r = root[r];
        }
        int i = x;
        while(i != r){
            int t = root[i];
            root[i] = r;
            i = t;
        }
        return r;
    }
    public void join(int X, int Y, int[] root){
        int rootX = find(X, root), rootY = find(Y, root);
        if(rootX != rootY){
          //build an edge between two islands and count--
            root[rootY] = rootX;
            count--;
        }
    }
    public int numIslands(char[][] grid) {
        if(grid == null || grid.length == 0){
            return 0;
        }
        int m = grid.length, n = grid[0].length;
        int[] root = new int[m * n];
        //init
        for(int i = 0; i < m * n; i++){
            root[i] = i;
            int x = i / n, y = i % n;
            if(grid[x][y] == '1'){
                count++;
            }
        }

        for(int i = 0; i < m * n; i++){
            int x = i / n, y = i % n;
            int down = x + 1, right = y + 1;
            if(down < m && grid[down][y] == '1' && grid[x][y] == '1'){
                join(i, i + n, root);
            }
            if(right < n && grid[x][y] == '1' && grid[x][right] == '1'){
                join(i, i + 1, root);
            }
        }

        return count;
    }
}
```
