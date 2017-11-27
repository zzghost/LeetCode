# Permutations
Given a collection of numbers that might contain duplicates, return all possible unique permutations.

For example,
[1,1,2] have the following unique permutations:
```
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]
```

## Solution
BackTracking.
```java
class Solution {
    List<List<Integer>> rst = new ArrayList<>();
    List<Integer> alist = new ArrayList<>();
    public void find(int[] nums, int position, int[] visited){
        if(position == nums.length){
            rst.add(new ArrayList<>(alist));
            return ;
        }
        for(int i = 0; i < nums.length; i++){
            if(visited[i] == 1) continue;
            if(i > 0 && nums[i - 1] == nums[i] && visited[i - 1] == 0) continue;
            alist.add(nums[i]);
            visited[i] = 1;
            find(nums, position + 1, visited);
            visited[i] = 0;
            alist.remove(alist.size() - 1);
        }
    }
    public List<List<Integer>> permuteUnique(int[] nums) {
        if(nums == null || nums.length == 0)
            return rst;
        Arrays.sort(nums);
        int[] visited = new int[nums.length];
        find(nums, 0, visited);
        return rst;
    }
}
```
