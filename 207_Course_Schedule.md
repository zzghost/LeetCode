# Course Schedule
## Description
There are a total of n courses you have to take, labeled from 0 to n - 1.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

Given the total number of courses and a list of prerequisite pairs, is it possible for you to finish all courses?

For example:
```
2, [[1,0]]
```
There are a total of 2 courses to take. To take course 1 you should have finished course 0. So it is possible.
```
2, [[1,0],[0,1]]
```
There are a total of 2 courses to take. To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.

Note:
1. The input prerequisites is a graph represented by a list of edges, not adjacency matrices. Read more about [how a graph is represented](https://www.khanacademy.org/computing/computer-science/algorithms/graph-representation/a/representing-graphs).
2. You may assume that there are no duplicate edges in the input prerequisites.

## Solution
It can be seen as searching circle in a graph.We can do this via DFS or BFS(Topological sort).  
1. Depth-first Search
```java
class Solution {
    public boolean dfs(ArrayList[] courseGraph, int[] visited, int idx){
        if(visited[idx] == 1){
            return false;
        }
        visited[idx] = 1;
        for(int i = 0; i < courseGraph[idx].size(); i++){
            if(!dfs(courseGraph, visited, (int)courseGraph[idx].get(i))){
                return false;
            }
        }
        visited[idx] = 0;
        return true;
    }
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        ArrayList[] courseGraph = new ArrayList[numCourses];
        for(int i = 0; i < numCourses; i++){
            courseGraph[i] = new ArrayList();
        }
        for(int i = 0; i < prerequisites.length; i++){
            courseGraph[prerequisites[i][1]].add(prerequisites[i][0]);
        }
        int[] visited = new int[numCourses];
        for(int i = 0; i < numCourses; i++){
            if(!dfs(courseGraph, visited, i)){
                return false;
            }
        }
        return true;
    }
}
```
2. Breadth-first Search.  
Use queue to store nodes with `indegree=0`.  
```java
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        ArrayList[] courseGraph = new ArrayList[numCourses];
        int[] degree = new int[numCourses];
        for(int i = 0; i < numCourses; i++){
            courseGraph[i] = new ArrayList();
        }
        for(int i = 0; i < prerequisites.length; i++){
            courseGraph[prerequisites[i][1]].add(prerequisites[i][0]);
            degree[prerequisites[i][0]]++;
        }
        Queue<Integer> queue = new LinkedList<>();
        int count = 0;
        for(int i = 0; i < degree.length; i++){
            if(degree[i] == 0){
                queue.offer(i);
                count++;
            }
        }
        while(!queue.isEmpty()){
            int tp = queue.poll();
            for(int i = 0; i < courseGraph[tp].size(); i++){
                int neighbor = (int)courseGraph[tp].get(i);
                degree[neighbor]--;
                if(degree[neighbor] == 0){
                    queue.offer(neighbor);
                    count++;
                }
            }
        }
        return (count == numCourses);
    }
}
```
