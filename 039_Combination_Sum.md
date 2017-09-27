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
