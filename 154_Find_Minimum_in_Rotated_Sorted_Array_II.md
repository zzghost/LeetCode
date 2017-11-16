# Find Minimum in Rotated Sorted Array II
Related problem:[153 Find Minimum in Rotated Sorted Array](https://github.com/zzghost/leetcode/blob/master/153_Find_Minimum_in_Rotated_Sorted_Array.md)
```
Follow up for "Find Minimum in Rotated Sorted Array":
What if duplicates are allowed?
Would this affect the run-time complexity? How and why?
```
Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., `0 1 2 4 5 6 7` might become `4 5 6 7 0 1 2`).

Find the minimum element.

The array may contain duplicates.

## Solution
Binary Search.  
**Complexity: Time O(logn), Space O(1).**
```java
class Solution {
    public int findMin(int[] nums) {
        if(nums == null || nums.length == 0)
            return 0;
        int low = 0, high = nums.length - 1;
        while(low < high - 1){
            int mid = (high - low) / 2 + low;
            if(nums[mid] < nums[high]){
                high = mid;
            }
            else if(nums[mid] > nums[high]){
                low = mid;
            }
            //skip the duplicates
            else
                high--;
        }
        return (nums[low] > nums[high]) ? nums[high] : nums[low];
    }
}
```
