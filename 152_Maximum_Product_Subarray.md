# Maximum Product Subarray
## Description
Find the contiguous subarray within an array (containing at least one number) which has the largest product.

For example, given the array `[2,3,-2,4]`,
the contiguous subarray `[2,3]` has the largest product = 6.

## Solution
1. Record(Naive solution).  
record[i] reprents the till `i`, the max product including the current `num[i]`  
**Complexity: Time O(n^2), Space O(n).**
```java
class Solution {
    public int findFirstNeg(int[] nums, int idx){
        int i = idx - 1;
        for(; i >= 0 && nums[i] > 0; i--);
        return (i >= 0) ? i : idx;
    }
    public int maxProduct(int[] nums) {
        int n = nums.length;
        int[] record = new int[n];
        record[0] = nums[0];
        int res = record[0];
        for(int i = 1; i < n; i++){
            if(nums[i] > 0 && record[i - 1] > 0)
                record[i] = record[i - 1] * nums[i];
            else if(nums[i] > 0 && record[i - 1] <= 0)
                record[i] = nums[i];
            else if(nums[i] < 0 && record[i - 1] < 0)
                record[i] = record[i - 1] * nums[i];
            else{
                int idx = findFirstNeg(nums, i);
                int product = 1;
                for(int j = idx; j <= i; j++)
                    product *= nums[j];
                if(idx > 0 && record[idx - 1] > 0)
                    product *= record[idx - 1];
                record[i] = product;
            }
            res = Math.max(res, record[i]);
        }
        return res;
    }
}
```
2. Dynamic Programming.
Local optimal and global optimal solution. Here, local optimal is definitely not global optimal since there's negtive ones. However, it's not every troublesome because we can keep `local maximum` as well as `local minumum`.  
So the state transition equation is:  
`max = max{nums[i], max{nums[i] * min, nums[i] * max}};`,  
`min = min{nums[i], min{nums[i] * tmp, nums[i] * min}};`
max and min are the local extreme value. Space has been optimized to O(1).  
**Complexity: Time O(n) Space O(1).**
```java
class Solution {
    public int maxProduct(int[] nums) {
        int n = nums.length;
        int max = nums[0], min = nums[0], res = max;
        for(int i = 1; i < n; i++){
            int tmp = max;
            max = Math.max(nums[i], Math.max(nums[i] * min, nums[i] * max));
            min = Math.min(nums[i], Math.min(nums[i] * tmp, nums[i] * min));
            res = Math.max(max, res);
        }
        return res;
    }
}
```
