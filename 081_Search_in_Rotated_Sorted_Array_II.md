# Search in Rotated Sorted Array II
## Description
Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., `0 1 2 4 5 6 7` might become `4 5 6 7 0 1 2`).

Write a function to determine if a given target is in the array.

The array may contain duplicates.

## Solution
Use once binary search.  
**Complexity: Time O(logn), Space O(1).**  
```java
class Solution {
    public boolean search(int[] nums, int target) {
        if(nums == null || nums.length == 0)
            return false;
        int n = nums.length, low = 0, high = n - 1;
        while(low <= high){
            int mid = (high - low) / 2 + low;
            if(nums[mid] == target)
                return true;
            //if mid is at the right part
            if(nums[mid] < nums[high] || nums[mid] < nums[low])
                if(target > nums[mid] && target <= nums[high])
                    low = mid + 1;
                else
                    high = mid - 1;
            //if mid is at the left part
            else if(nums[mid] > nums[high] || nums[mid] > nums[low])
                if(target < nums[mid] && target >= nums[low])
                    high = mid - 1;
                else
                    low = mid + 1;
            else//skip the duplicate
                low++;//or high--;
        }
        return false;
    }
}
```
