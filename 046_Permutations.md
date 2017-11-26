# Permutations
## Description
Given a collection of distinct numbers, return all possible permutations.

For example,
`[1,2,3]` have the following permutations:
```
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```
## Solution
BackTracking.  
**Complexity: Time O(nlogn), Space O(n).**
```java
class Solution {
    List<List<Integer>> rst = new ArrayList<>();
    public void find(int[] nums, int position, List<Integer> aList, int[] visit){
        if(position >= nums.length){
            rst.add(new ArrayList<>(aList));
            return ;
        }
        for(int i = 0; i < nums.length; i++){
            if(visit[i] == 1)
                continue;
            visit[i] = 1;
            aList.add(nums[i]);
            find(nums, position+1, aList,visit);
            visit[i] = 0;
            aList.remove(aList.size() - 1);
        }

    }
    public List<List<Integer>> permute(int[] nums) {
        if(nums == null || nums.length == 0)
            return rst;
        int n = nums.length;
        int[] visit = new int[n];
        List<Integer> aList = new ArrayList<>();
        find(nums, 0, aList,visit);
        return rst;
    }
}
```
