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
1. BackTracking
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
2. Bit Manipulation
Example: `[1, 2, 3]`
subsets: `[]` = 0 = (000)2, `[3]` = 1 = (001)2, `[2]` = 2 = (010)2, `[1]` = 3 = (100)2  
There are 2^n subsets.  
Use each number and each element do `and` operation.  
```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        int n = nums.length;
        List<List<Integer>> rst = new ArrayList<>();
        int allSets = 1 << n;//2^n
        for(int i = 0; i < allSets; i++){
            List<Integer> aList = new ArrayList<>();
            for(int j = 0; j < n; j++){
              //i is subset's number, (1 << j) is the element
                if(((1 << j) & i) != 0){
                    aList.add(nums[j]);
                }

            }
            rst.add(aList);
        }
        return rst;
    }
}
```
