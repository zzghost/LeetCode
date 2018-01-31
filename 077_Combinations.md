# Combinations
Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

For example,
If n = 4 and k = 2, a solution is:
```
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```
## Solution
```java
class Solution {
    List<List<Integer>> combi = new ArrayList<>();
    public void find(int n, int k, int count, int idx, int[] visit, List<Integer> list){
        if(count == k){
            combi.add(new ArrayList<>(list));
            list = new ArrayList<>();
            return ;
        }
        for(int i = idx + 1; i <= n; i++){
            if(visit[i - 1] == 0){
                list.add(i);
                visit[i - 1] = 1;
                find(n, k, count+1, i, visit, list);
                visit[i - 1] = 0;
                list.remove(list.size() - 1);
            }
        }
    }
    public List<List<Integer>> combine(int n, int k) {
        if(n < k) return combi;
        int[] visit = new int[n];
        List<Integer> list = new ArrayList<>();
        find(n, k, 0, 0, visit, list);
        return combi;
    }
}
```
