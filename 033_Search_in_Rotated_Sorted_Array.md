# Search in Roated Sorted Array

## Description
Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.  

(i.e., `0 1 2 4 5 6 7` might become `4 5 6 7 0 1 2`).  

You are given a target value to search. If found in the array return its index, otherwise return -1.  

You may assume no duplicate exists in the array.  

## Solution
One basic solution has 3 steps:
1. Use binary search to find the pivot.  
2. If low < target && pivot > target, search [low, pivot)
3. else search [pivot, high)
Here we can use only one binary search.  
**Complexity: Time O(logn), Space O(1).**
```java
public int search(int[] nums, int target) {
    if(nums == null || nums.length == 0)
        return -1;

    int low = 0, high = nums.length - 1;
    while(low < high){
        int mid = (high - low) / 2 + low;

        if(nums[mid] == target)
            return mid;

        if(nums[mid] < target){
            if(nums[mid] > nums[low] || nums[high] >= target)
                low = mid + 1;
            else
                high = mid - 1;
        }
        else{
            if(nums[mid] >= nums[low]){
                if(nums[low] <= target)
                    high = mid - 1;
                else if(nums[high] >= target)
                    low = mid + 1;
                else
                    break;
            }
            else
                high = mid - 1;
        }
    }
    return (nums[low] == target) ? low : -1;
}
```
