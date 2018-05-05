## Description
Given a set of candidate numbers (C) (without duplicates) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.

The same repeated number may be chosen from C unlimited number of times.

**Note:**  
+ All numbers (including target) will be positive integers.
+ The solution set must not contain duplicate combinations.
For example, given candidate set ``[2, 3, 6, 7]`` and target `7`,
A solution set is:
```
[
  [7],
  [2, 2, 3]
]
```
## Solution
Backtracking.  
**Complexity: Time O(n2^n), Space O(n)**
```java
List<List<Integer>> rst = new ArrayList<List<Integer>>();
List<Integer> aList = new ArrayList<>();

public void find(int[] candidates, int target, int idx){
    if(target > 0)
        for(int i = idx; i < candidates.length && target >= candidates[i]; i++){
            aList.add(candidates[i]);
            find(candidates, target - candidates[i], i);
            aList.remove(aList.size() - 1);
        }
    else if(target == 0)
        rst.add(new ArrayList<Integer>(aList));

}
public List<List<Integer>> combinationSum(int[] candidates, int target) {
    Arrays.sort(candidates);
    find(candidates, target, 0);
    return rst;
}
```
