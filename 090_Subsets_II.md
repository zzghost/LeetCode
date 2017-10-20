# Subsets II
Related problem: [078 Subsets](https://github.com/zzghost/leetcode/blob/master/078_Subsets.md)
## Description
Given a collection of integers that might contain duplicates, nums, return all possible subsets.

**Note:** The solution set must not contain duplicate subsets.

For example,
If *nums* = [1,2,2], a solution is:
```
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```
## Solution
DFS, BackTracking.  
**Complexity: Time O(2^n), Space O(2^n).**
```java
class Solution {
    List<List<Integer>> rst = new ArrayList<List<Integer>>();
    public void find(int[] nums, int idx, List<Integer> aList){
        //add to the final list
        rst.add(new ArrayList<>(aList));

        for(int i = idx; i < nums.length; i++){
          //skip the duplicates
            if(i > idx && nums[i] == nums[i - 1])
                continue ;
            aList.add(nums[i]);
            find(nums, i + 1, aList);
            aList.remove(aList.size() - 1);
        }
    }
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<Integer> aList = new ArrayList<Integer>();
        Arrays.sort(nums);
        find(nums, 0, aList);
        return rst;
    }
}
```
