# Remove Duplicates from Sorted Array II
## Description
Follow up for "Remove Duplicates":  
What if duplicates are allowed at most twice?  

## Example
```
Given sorted array nums = [1,1,1,2,2,3],

Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3. It doesn't matter what you leave beyond the new length.  
```
## Solution
Basic Traversal.  
**Complexity: Time O(n), Space O(1).**
```java
public int removeDuplicates(int[] nums) {
    if(nums == null || nums.length == 0)
        return 0;

    int countLength = 0, i, j;
    for(i = 0, j = 0; i < nums.length - 2; i++){
        if(nums[i] != nums[i + 2])
            nums[j++] = nums[i];
    }
    if(i < nums.length){
        nums[j++] = nums[i++];
    }
    if(i < nums.length){
        nums[j] = nums[i];
    }
    return j + 1;
}
```
