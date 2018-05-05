# Maximum Subarray  
## Description  
Find the contiguous subarray within an array (containing at least one number) which has the largest sum.  
## Example  
> given the array [-2,1,-3,4,-1,2,1,-5,4],  
> the contiguous subarray [4,-1,2,1] has the largest sum = 6.

## Solution  
Dynamic programming.  
dp[i] = max(dp[i-1] + nums[i], nums[i])  
the first item means nums[i] is in the continuous pre-subarray.  
the second item means nums[i] is the first num in the continuous subarray.  
As the dp[i] only depends on the dp[i-1], we can use one varible instead of dp[nums.length], which decreases the space complexity from O(n) to O(1).  
Complexity: Time O(n), Space O(1)  
```java
    public int maxSubArray(int[] nums) {
        int aws = nums[0], pre = nums[0];
        for(int i = 1; i < nums.length; i++){
            pre = Math.max(pre + nums[i], nums[i]);
            aws = Math.max(aws, pre);
        }
        return aws;
    }
```
