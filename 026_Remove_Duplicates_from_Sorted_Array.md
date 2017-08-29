# Remove Duplicates from Sorted Array  
## Description  
Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length.  
Do not allocate extra space for another array, you must do this in place with constant memory.  
## Example  
> Given input array nums = [1,1,2], 
> Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively. It doesn't matter what you leave beyond the new length.  
## Solution  
Basic Traversal.  
Complexity:Time O(n), Space O(1)  
```java
public int removeDuplicates(int[] nums) {
    if(nums == null || nums.length == 0) return 0;
    int count = 0, len = nums.length;
    for(int i = 1; i < len; i++){
        if(nums[i] != nums[count]){
            nums[++count] = nums[i];
        }
    }
    return count+1;
}
```
