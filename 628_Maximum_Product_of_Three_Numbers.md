# Maximum Product of Three Numbers
## Description
Given an integer array, find three numbers whose product is maximum and output the maximum product.  
## Example
**Example 1:**  
```
Input: [1,2,3]  
Output: 6  
```
**Example 2:**  
```
Input: [1,2,3,4]  
Output: 24  
```
**Note:**  

1. The length of the given array will be in range [3,104] and all elements are in the range [-1000, 1000].  
2. Multiplication of any three numbers in the input won't exceed the range of 32-bit signed integer.  

## Solution
1. Sorting. 
Complexity: Time O(nlogn), Space O(logn).(Sorting takes extra space O(logn) and extra time O(nlogn))  
```java
public int maximumProduct(int[] nums) {
    Arrays.sort(nums);
    return Math.max(nums[0] * nums[1] * nums[nums.length - 1], nums[nums.length - 1] * nums[nums.length - 2] * nums[nums.length - 3]);
}
```
2. Single Scan.(Optimal)  
No need to sorting. We observed that result depends only on the smallest, the second smallest, the largest, the 2nd largest, and the 3rd largest. Thus, we use 5 variables to record.  
Complexity: Time O(n), Space O(1).  
```java
public int maximumProduct(int[] nums) {
    int min1, min2, max1, max2, max3;
    min1 = min2 = Integer.MAX_VALUE;
    max1 = max2 = max3 = Integer.MIN_VALUE;
    for(int num : nums){
    //num is smaller than the current smallest.
        if(num <= min1){
            min2 = min1;
            min1 = num;
        }
    //num is between smallest and second smallest.
        else if(num <= min2){
            min2 = num;
        }
    //num is larger than the largest.
        if(num >= max1){
            max3 = max2;
            max2 = max1;
            max1 = num;
        }
    //num is between largest and second largest.
        else if(num >= max2){
            max3 = max2;
            max2 = num;
        }
    //num is larger than the third largest.
        else if(num >= max3)
            max3 = num;
    }
    return Math.max(min1 * min2 * max1, max1 * max2 * max3);
}
```
