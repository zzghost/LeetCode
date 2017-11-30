# Single Number
## Description
Given an array of integers, every element appears twice except for one. Find that single one.

**Note:**  
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?
## Solution
```java
class Solution {
    public int singleNumber(int[] nums) {
        int x = nums[0];
        for(int i = 1; i < nums.length; i++){
            x  ^= nums[i];
        }
        return x;
    }
}
```
