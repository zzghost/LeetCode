# Search for a Range
## Description
Given an array of integers sorted in ascending order, find the starting and ending position of a given target value.  

Your algorithm's runtime complexity must be in the order of O(log n).  

If the target is not found in the array, return [-1, -1].  

For example,  
```
Given [5, 7, 7, 8, 8, 10] and target value 8,
return [3, 4].
```
## Solution
1. Traversal.(Not optimal)
**Complexity: Time O(n), Space O(1).**
```java
public int[] searchRange(int[] nums, int target) {
    int[] rst = {-1, -1};
    if(nums == null || nums.length == 0)
        return rst;

    int low = 0, high = nums.length - 1;
    while(low <= high){
        while(low < nums.length && nums[low] < target )
            low++;
        while(high >= 0 && nums[high] > target )
            high--;
        if(low < nums.length && high >= 0 && nums[low] == target && nums[high] == target){
            rst[0] = low;
            rst[1] = high;
            return rst;
        }

    }
    return rst;
}
```
2. Two Binary Search.
Use binary search to find left bound and right bound respectively.  
**Complexity: Time O(logn), Space O(1).**
```java
class Solution {
    public int leftBound(int[] nums, int target){
        int low = 0, high = nums.length - 1;
        while(low <= high){
            int mid = (high - low) / 2 + low;
            if(nums[mid] == target){
                if(mid == 0 || nums[mid - 1] < target){
                    return mid;
                }
                high = mid - 1;
            }
            else if(nums[mid] > target){
                high = mid - 1;
            }
            else{
                low = mid + 1;
            }
        }
        return -1;
    }
    public int rightBound(int[] nums, int target){
        int low = 0, high = nums.length - 1;
        while(low <= high){
            int mid = (high - low) / 2 + low;
            if(nums[mid] == target){
                if(mid == nums.length - 1 || nums[mid + 1] > target){
                    return mid;
                }
                low = mid + 1;
            }
            else if(nums[mid] > target){
                high = mid - 1;
            }
            else{
                low = mid + 1;
            }
        }
        return -1;
    }
    public int[] searchRange(int[] nums, int target) {   
        int[] rst = new int[2];
        rst[0] = leftBound(nums, target);
        rst[1] = rightBound(nums, target);
        return rst;
    }
}
```
