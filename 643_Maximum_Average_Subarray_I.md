# Maximum Average Subarray I
## Description
Given an array consisting of n integers, find the contiguous subarray of given length k that has the maximum average value. And you need to output the maximum average value.  
## Example
```
Input: [1,12,-5,-6,50,3], k = 4  
Output: 12.75  
Explanation: Maximum average is (12-5-6+50)/4 = 51/4 = 12.75  
```
**Note:**  
1. 1 <= k <= n <= 30,000.  
2. Elements of the given array will be in the range [-10,000, 10,000].  
## Solution
1. Slide Window  
Complexity: Time O(n), Space O(1)  
```java
public double findMaxAverage(int[] nums, int k) {
    int curr = 0;
    for(int j = 0; j < k; j++)
        curr += nums[j];
    int max = curr;
    for(int i = k; i < nums.length; i++){
        curr +=  nums[i] - nums[i - k];
        max = Math.max(max, curr);
    }
    return (double)max / k;
}
```
2. Cumulative Sum  
Complexity: Time O(n), Space O(n)  
```java
public double findMaxAverage(int[] nums, int k) {
    int[] cumuSum = new int[nums.length];
    cumuSum[0] = nums[0];
    for(int i = 1; i < nums.length; i++)
        cumuSum[i] = cumuSum[i - 1] + nums[i];
    
    int max = cumuSum[k - 1];
    for(int i = k; i < nums.length; i++)
        max = Math.max(max, cumuSum[i] - cumuSum[i - k]);
    return (double)max / k;
}
