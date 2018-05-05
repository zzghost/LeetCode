# Friend Circles
## Description
There are N students in a class. Some of them are friends, while some are not. Their friendship is transitive in nature. For example, if A is a direct friend of B, and B is a direct friend of C, then A is an indirect friend of C. And we defined a friend circle is a group of students who are direct or indirect friends.

Given a N*N matrix M representing the friend relationship between students in the class. If M[i][j] = 1, then the ith and jth students are direct friends with each other, otherwise not. And you have to output the total number of friend circles among all the students.

**Example 1:**  
```
Input:
[[1,1,0],
 [1,1,0],
 [0,0,1]]
Output: 2
Explanation:The 0th and 1st students are direct friends, so they are in a friend circle.
The 2nd student himself is in a friend circle. So return 2.
```
**Example 2:**  
```
Input:
[[1,1,0],
 [1,1,1],
 [0,1,1]]
Output: 1
Explanation:The 0th and 1st students are direct friends, the 1st and 2nd students are direct friends,
so the 0th and 2nd students are indirect friends. All of them are in the same friend circle, so return 1.
```
**Note:**  
1. N is in range [1,200].
2. M[i][i] = 1 for all students.
3. If M[i][j] = 1, then M[j][i] = 1.

## Solution
Union Find.  
**Complexity: O(n^2), O(n).**  
```java
class Solution {
    private int group = 0;
    public int find(int x, int[] pre){
        int root = x;
        while(pre[root] != root){
            root = pre[root];
        }
        int i = x, j;
        while(i != root){
            j = pre[i];
            pre[i] = root;
            i = j;
        }
        return root;
    }
    public void join(int x, int y, int[] pre){
        int rootX = find(x, pre), rootY = find(y, pre);
        if(rootX != rootY){
            pre[rootX] = rootY;
            group--;
        }
    }
    public int findCircleNum(int[][] M) {
        if(M == null || M.length == 0){
            return 0;
        }
        int[] pre = new int[M.length];
        for(int i = 0; i < M.length; i++){
            pre[i] = i;
        }
        group = M.length;
        for(int i = 0; i < M.length; i++){
            for(int j = 0; j < M.length; j++){
                if(M[i][j] == 1){
                    join(i, j, pre);
                }
            }
        }

        return group;
    }
}
```
