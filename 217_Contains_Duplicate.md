# Contains Duplicate  
## Description
Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.  
## Solution  
Sorting.  
Complexity: Time O(nlogn), Space O(1).  
Another approach is using HashTable.  
```java
public boolean containsDuplicate(int[] nums) {
    if(nums == null || nums.length == 0) return false;
    int len = nums.length;
    Arrays.sort(nums);
    for(int i = 0; i < len - 1; i++){
        if(nums[i] == nums[i+1])
            return true;
    }
    return false;
}
```
