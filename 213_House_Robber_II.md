# House Robber II
## Description
Note: This is an extension of [House Robber](https://leetcode.com/problems/house-robber/).

After robbing those houses on that street, the thief has found himself a new place for his thievery so that he will not get too much attention. This time, all houses at this place are arranged in a circle. That means the first house is the neighbor of the last one. Meanwhile, the security system for these houses remain the same as for those in the previous street.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

## Solution
Dynamic Programming.  
Count `with first element` and `without first element` situation.  
Then take max of them.  
```java
class Solution {
    public int[] plan(int[] nums, int start, int end){
        int[] dp = new int[end - start + 1];
        dp[0] = nums[start];
        dp[1] = Math.max(nums[start], nums[start + 1]);
        for(int i = 2; i <= end - start; i++){
            dp[i] = Math.max(nums[i + start] + dp[i - 2], dp[i - 1]);
        }
        return dp;
    }
    public int rob(int[] nums) {
        if(nums == null || nums.length == 0){
            return 0;
        }
        if(nums.length == 1){
            return nums[0];
        }
        if(nums.length == 2){
            return Math.max(nums[0], nums[1]);
        }
        if(nums.length == 3){
            return Math.max(nums[0], Math.max(nums[1], nums[2]));
        }
        int n = nums.length;
        int[] noFirst = plan(nums, 1, n - 1);
        int[] withFirst = plan(nums, 0, n - 1);

        int rst = Math.max(nums[n - 1] + noFirst[n - 4], withFirst[n - 2]);

        return rst;
    }
}
```
