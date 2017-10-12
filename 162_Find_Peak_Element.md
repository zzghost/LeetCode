# Find Peak Element
## Description
A peak element is an element that is greater than its neighbors.  

Given an input array where num[i] ≠ num[i+1], find a peak element and return its index.  

The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.  

You may imagine that num[-1] = num[n] = -∞.  

For example, in array [1, 2, 3, 1], 3 is a peak element and your function should return the index number 2.  

**Note:**
Your solution should be in logarithmic complexity.
## Solution
**Complexity: Time O(logn), Space O(1).**
```java
public int findPeakElement(int[] nums) {
    int n = nums.length;
    if(n <= 1)
        return 0;
    int low = 0, high = n - 1;
    while(low < high){
        int mid = (high - low) / 2 + low;
        if((mid == 0 || nums[mid] > nums[mid - 1]) && (mid == n - 1 || nums[mid] > nums[mid + 1]))
            return mid;
        if(mid == 0 || nums[mid] > nums[mid - 1])
            low = mid + 1;
        else
            high = mid;
    }
    return low;
}
```
