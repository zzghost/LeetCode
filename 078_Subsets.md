# Subsets
## Description
Given a set of distinct integers, nums, return all possible subsets.  

**Note:** The solution set must not contain duplicate subsets.  
## Example
If nums = `[1,2,3]`, a solution is:  
```
[
[3],
[1],
[2],
[1,2,3],
[1,3],
[2,3],
[1,2],
[]
]
```
## Solution
DFS
**Complexity: Time O(2^n), Space O(2^n).**
```java
public void findsubsets(int[] nums, int idx, List<Integer> aList, List<List<Integer>> allSubsets){
    if(idx >= nums.length){
        allSubsets.add(new ArrayList<Integer>(aList));
        return;
    }

    aList.add(nums[idx]);
    findsubsets(nums, idx + 1, aList, allSubsets);
    aList.remove(aList.size() - 1);
    findsubsets(nums, idx + 1, aList, allSubsets);
}
public List<List<Integer>> subsets(int[] nums) {
    List<List<Integer>> allSubsets = new ArrayList<>();
    List<Integer> aList = new ArrayList<>();

    findsubsets(nums, 0, aList, allSubsets);

    return allSubsets;
}
```
