# Move Zeroes
## Description
Given an array `nums`, write a function to move all `0`'s to the end of it while maintaining the relative order of the non-zero elements. 
## Example
> For example, given `nums = [0, 1, 0, 3, 12]`, after calling your function, `nums` should be `[1, 3, 12, 0, 0]`. 
## Solution
1. Two Pointers(Space Optimal, Operation Sub-Optimal)  
One pointer to put non-zero numbers, while another pointer is traversal.  
Complexity: Time O(n), Space O(1)  
```java
public void moveZeroes(int[] nums) {
    for(int i = 0, k = 0; i < nums.length;i++)
        if(nums[i] != 0)
            nums[k++] = nums[i];
        for(int i = k; i < nums.length;i++)
            nums[i] = 0;
}
```
2. Two Pointers(Optimal)  
One pointer *k* to put non_zero numbers, while numbers between *k* and traversal pointer *i* are zero.  
Complexity: Time O(n), Space O(1)
```java
public void moveZeroes(int[] nums) {
    for(int i = 0, k = 0; i < nums.length; i++){
        if(nums[i] != 0){
            int tmp = nums[i];
            nums[i] = nums[k];
            nums[k++] = tmp;
        }
    }
}
```
