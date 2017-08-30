# Search Insert Position 
## Description
Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.  
You may assume no duplicates in the array.  
## Example
> [1,3,5,6], 5 → 2
> [1,3,5,6], 2 → 1
> [1,3,5,6], 7 → 4
> [1,3,5,6], 0 → 0 
## Solution 
Binary Search.
```java
public int searchInsert(int[] nums, int target) {
    if(nums == null || nums.length == 0)
        return 0;
    int low = 0, high = nums.length - 1;
    while(low < high){
        int mid = (low + high - 1) / 2;
        if(nums[mid] == target)
            return mid;
        if(nums[mid] < target)
            low = mid + 1;
        else
            high = mid - 1;
    }
    if(nums[low] < target)
        return low + 1;
    else
        return low;
}
```
