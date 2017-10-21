# 3Sum Closest
## Description
Given an array S of n integers, find three integers in S such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.
```
For example, given array S = {-1 2 1 -4}, and target = 1.

The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```
## Solution
Just like [015 3Sum](https://github.com/zzghost/leetcode/blob/master/015_3Sum.md), Use Two pointers.  
**Complexity: Time O(n^2), Space O(1).**
```java
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        Arrays.sort(nums);
        int n = nums.length;
        long res = Integer.MAX_VALUE;
        for(int i = 0; i + 2 < n; i++){
            if(i > 0 && nums[i] == nums[i - 1])
                continue ;
            int j = i + 1, k = n - 1;
            while(j < k){
                int sum = nums[i] + nums[j] + nums[k];
                if(sum == target) {res = sum; break;}
                if(Math.abs(res - target) > Math.abs(sum - target)){
                    res = sum;
                }
                if(sum > target){
                    k--;
                    //skip the duplicates
                    while(k > j && nums[k] == nums[k + 1]) k--;
                }
                else{
                    j++;
                    //skip the duplicates
                    while(k > j && nums[j] == nums [j - 1]) j++;
                }
            }
        }
        return (int)res;
    }
}
```
