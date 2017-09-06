# Subarray Sum Equals K  
## Description
Given an array of integers and an integer k, you need to find the total number of continuous subarrays whose sum equals to k.  
## Example
**Example 1:**
```
Input:nums = [1,1,1], k = 2  
Output: 2  
```
**Note:**  

1. The length of the array is in range [1, 20,000].  
2. The range of numbers in the array is [-1000, 1000] and the range of the integer k is [-1e7, 1e7].  

## Solution
1. Brute Force.  
**Complexity: Time O(n^2), Space O(1)**  
```java
public int subarraySum(int[] nums, int k) {
    if(nums == null || nums.length == 0) return 0;
    int n = nums.length, count = 0;
    for(int i = 0; i < n; i++){
        int sum = 0;
        for(int j = i; j < n; j++){
            sum += nums[j];
            if(sum == k){
                count++;
            }
        }
    }
    return count;
}
```
2. Using HashMap.  
Solution 1 calculates sum[i..j] == k. We can optimize the solution by calculating `sum[0..i-1]` and `sum[0..j]`.  
We use `HashMap` to save value `sum[0..m]`.  
**Complexity: Time O(n), Space O(n).**  
```java
public int subarraySum(int[] nums, int k) {
    if(nums == null || nums.length == 0) return 0;
    int n = nums.length, count = 0;
    Map<Integer, Integer> map = new HashMap<Integer, Integer>();
    map.put(0, 1);
    int sum = 0;
    for(int x : nums){
        sum += x;
        if(map.containsKey(sum - k))
            count += map.get(sum - k);
        map.put(sum, map.getOrDefault(sum, 0) + 1);
    }
    return count;
}

