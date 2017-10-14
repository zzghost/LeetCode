# Minimum Size Subarray Sum
## Description
Given an array of n positive integers and a positive integer s, find the minimal length of a contiguous subarray of which the sum ≥ s. If there isn't one, return 0 instead.  

For example, given the array [2,3,1,2,4,3] and s = 7,  
the subarray [4,3] has the minimal length under the problem constraint.  

**More practice:**
If you have figured out the O(n) solution, try coding another solution of which the time complexity is O(n log n).  

## Solution
1. Sliding window.
Window size is not a fixed number. Each sliding, it uses `sum>=s` to fix the window, and it remove the first element in the window.  
In other words, the window's length is not fixed, but the window's sum can satisfy the condition.  
**Complexity: Time O(n), Space O(1).**
```java
public int minSubArrayLen(int s, int[] nums) {
    if(nums == null || nums.length == 0)
        return 0;

    int n = nums.length;
    int minLen = Integer.MAX_VALUE;
    int sum = 0, length = 0;

    for(int i = 0, j = i; i < n; i++){
        while(j < n && sum < s){
            sum += nums[j];
            length++; j++;
        }
        if(sum >= s)
            minLen = Math.min(minLen, length);
        //remove the first element in the window
        sum -= nums[i];
        length--;
    }
    if(sum >= s)
        minLen = Math.min(minLen, length);
    return (minLen == Integer.MAX_VALUE) ? 0 : minLen;
}
```
2. Binary Search for sliding window.
Use binary search to find the window size, and then check if there's a satisfied answer.  
In other words, the window's length is fixed, but wheather the window has the answer is not sure.  
**Complexity: Time O(nlogn), Space O(1).**
```java
public boolean canFormSub(int size, int[] nums, int s){
    int sum = 0;
    for(int i = 0; i < nums.length; i++){
        if(i >= size)
            sum -= nums[i - size];
        sum += nums[i];
        if(sum >= s)
            return true;
    }
    return false;
}
public int minSubArrayLen(int s, int[] nums) {
    if(nums == null || nums.length == 0)
        return 0;

    int n = nums.length, minLen = 0;

    int low = 1, high = n;
    while(low <= high){
        int mid = (high - low) / 2 + low;
        //window size is mid, check if there's an answer in it.
        if(canFormSub(mid, nums, s)){
            minLen = mid;
            high = mid - 1;
        }
        else
            low = mid + 1;
    }
    return minLen;
}
```
