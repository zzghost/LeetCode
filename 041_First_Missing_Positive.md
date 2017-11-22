# First Missing Positive
## Description
Given an unsorted integer array, find the first missing positive integer.

For example,
Given `[1,2,0]` return `3`,
and `[3,4,-1,1]` return `2`.

Your algorithm should run in O(n) time and uses constant space.

## Solution
```java
class Solution {
    public int firstMissingPositive(int[] nums) {
        if(nums == null || nums.length == 0)
            return 1;
        int n = nums.length;
        for(int i = 0; i < n; ){
            if(nums[i] != i){
                if(nums[i] < n && nums[i] >= 0 && nums[nums[i]] != nums[i]){
                    int tmp = nums[i];
                    nums[i] = nums[tmp];
                    nums[tmp] = tmp;
                }
                else{
                    i++;
                }
            }
            else
                i++;
        }
        //check
        int i = 1;
        for(; i < n; i++){
            if(nums[i] != i){
                return i;
            }
        }
        return (nums[0] != n) ? n : n + 1;
    }
}
```
