# Jump Game
## Description
Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

For example:
A = `[2,3,1,1,4]`, return true.

A = `[3,2,1,0,4]`, return false.
## Solution
From back to start.  
If there's zero, skip and count the number.  
Then find if there's a height to skip the zero fields.  
**Complexity: Time O(n), Space O(1).**
```java
class Solution {
    public boolean canJump(int[] nums) {
        if(nums == null || nums.length == 0)
            return false;
        int n = nums.length;
        if(n == 1)
            return true;
        int i = n - 2;
        while(i > 0){
            if(nums[i] >= 1){
                i--;
            }
            else{
                int start = i;
                //skip zero
                while(i > 0 && nums[i] == 0)
                    i--;
                //find if there's a height to skip the zeroes.
                while(i > 0 && nums[i] <= (start - i))
                    i--;
                //not found.
                if(i == 0 && nums[0] <= (start - i))
                    return false;
            }
        }
        return (nums[0] >= 1);
    }
}
```
