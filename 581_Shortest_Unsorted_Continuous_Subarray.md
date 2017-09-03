# Shortest Unsorted Continuous Subarray
## Description
Given an integer array, you need to find one continuous subarray that if you only sort this subarray in ascending order, then the whole array will be sorted in ascending order, too.  

You need to find the shortest such subarray and output its length.  
## Example
**Example 1:**  
```
Input: [2, 6, 4, 8, 10, 9, 15]  
Output: 5  
Explanation: You need to sort [6, 4, 8, 10, 9] in ascending order to make the whole array sorted in ascending order.  
```
**Note:**  
1. Then length of the input array is in range [1, 10,000].  
2. The input array may contain duplicates, so ascending order here means <=.  
## Solution
1. Sorting.  
Complexity: Time O(nlogn), Space O(n). Both for sorting.
```java
public int findUnsortedSubarray(int[] nums) {
    int[] sortedNums = Arrays.copyOf(nums, nums.length);
    Arrays.sort(sortedNums);
    int start = 0, end = 0, i, j;
    for(i = 0; i < nums.length; i++){
        if(nums[i] != sortedNums[i]){
            start = i;
            break;
        }
    }
    for(j = nums.length - 1; j >= 0; j--){
        if(nums[j] != sortedNums[j]){
            end = j;
            break;
        }
    }
    if(i == nums.length && j == -1)
        return 0;
    else
        return end - start + 1;
}
```
2. Two pointers.(Optimal)  
Complexity: Time O(n), Space O(1).  
```java
public int findUnsortedSubarray(int[] nums) {
    int n = nums.length, start = -1, end = -2, max = nums[0], min = nums[n - 1];
    for(int i = 1; i < n; i++){
        max = Math.max(nums[i], max);
        min = Math.min(nums[n - i - 1], min);
        if(nums[i] < max) end = i;
        if(nums[n - i - 1] > min) start = n - i - 1;
    }
    //Array is non-decreasing
    if(end < start && start < 0)
        return 0;
    else
        return end - start + 1;
}
```
