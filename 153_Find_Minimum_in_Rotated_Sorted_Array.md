# Find Minimum in Rotated Sorted Array 
## Description
Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.  

(i.e.,` 0 1 2 4 5 6 7` might become `4 5 6 7 0 1 2`).  

Find the minimum element.  

You may assume no duplicate exists in the array.  

## Solution
1. Basic Traversal.  
Easy to come up with this solution. However, binary search is faster.  
**Complexity: Time O(n), space O(1).**
```java
public int findMin(int[] nums) {
    int i = 0;
    for(; i < nums.length - 1 && nums[i] <= nums[i + 1]; i++);
    if (i < nums.length - 1) 
        return nums[i + 1]; 
    else return nums[0];
}
```
2. Binary Search.(Optimal)  
`nums[mid] < nums[high]` means we are at the smaller part, so go left then.  
`nums[mid] >= nums[high]` means we are at the larger part, so go right.  
**Complexity: Time O(logn), Space O(1).**  
```java
public int findMin(int[] nums) {
    if(nums == null || nums.length == 0)
        return 0;
    if(nums.length == 1)
        return nums[0];
    int low = 0, high = nums.length - 1;
    //while stops at low == high - 1,all we need to do is performing check "if(nums[low] > nums[high])" expression.
    while(low < high - 1){
        int mid = low + (high - low) / 2;
        if(nums[mid] < nums[high])
            high = mid;
        else
            low = mid;
    }
    if(nums[low] > nums[high])
        return nums[high];
    else
        return nums[low];
}
