# Combination SumII
## Description
Given a collection of candidate numbers (C) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.

Each number in C may only be used once in the combination.

**Note:**
All numbers (including target) will be positive integers.
The solution set must not contain duplicate combinations.
For example, given candidate set `[10, 1, 2, 7, 6, 1, 5]`and target `8`,
A solution set is:
```
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
```

## Solution
Backtracking.DFS.  
Same solution as [039 Combination Sum](https://github.com/zzghost/leetcode/blob/master/039_Combination_Sum.md)  
Here we needs to skip the duplicate.  
`if(i > idx) && candidates[i] == candidates[i - 1]` solves it.`i > idx` means candidates[i-1] is not added to the path, so if `candidates[i] == candidates[i-1]`, we should not add candidates[i].  
Take (1, 1, 6), target = 8 as an example. When it met first 1, it will add first 1, and then the path went down and finally (1,1,6) will be added to the final list. However, when it met second 1, it will skip it.    
**Complexity: Time O(2^n).**
```java
class Solution {
    List<List<Integer>> rst = new ArrayList<>();
    List<Integer> aList = new ArrayList<>();
    public void find(int[] candidates, int target, int idx){
        if(target > 0){
            for(int i = idx; i < candidates.length; i++){
              //skip the duplicates
                if(i > idx && candidates[i] == candidates[i - 1]){
                    continue;
                }
                aList.add(candidates[i]);
                find(candidates, target - candidates[i], i + 1);
                aList.remove(aList.size() - 1);
            }
        }
        else if(target == 0){
            rst.add(new ArrayList<>(aList));
        }
    }
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        Arrays.sort(candidates);
        find(candidates, target, 0);
        return rst;
    }
}
```
