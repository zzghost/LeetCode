# Longest Increasing Subsequence
## Solution

1. Dynamic Programming  
dp[i] denotes the longest length in the end of nums[i].  
dp[i] depends on max(dp[0..i-1]).  
**Complexity: Time O(n^2), Space O(n).**   
```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        if(nums == null || nums.length == 0){
            return 0;
        }
        int n = nums.length;
        int[] dp = new int[n];
        dp[0] = 1;
        int LIS = 1;
        for(int i = 1; i < n; i++){
            dp[i] = 1;
            for(int j = 0; j < i; j++){
                if(nums[i] > nums[j] && dp[i] < dp[j] + 1){
                    dp[i] = dp[j] + 1;
                }
            }
            if(LIS < dp[i]){
                LIS = dp[i];
            }
        }
        return LIS;
    }
}
```

2. Use stack  
1)Not-optimal  
The stack stores the numbers in LIS.  
If nums[i] is larger than top element of the stack, push nums[i] into the stack;  
else, find the first position where nums[i] can replace the nums[j].  
**Complexity: Time O(n^2), Space O(n).**  
```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        if(nums == null || nums.length == 0){
            return 0;
        }
        ArrayList<Integer> sequence = new ArrayList<>();
        sequence.add(nums[0]);
        for(int i = 1; i < nums.length; i++){
            if(nums[i] > sequence.get(sequence.size() - 1)){
                sequence.add(nums[i]);
            }
            else{
                for(int j = 0; j < sequence.size(); j++){
                    if(sequence.get(j) >= nums[i]){
                        sequence.set(j, nums[i]);
                        break;
                    }
                }
            }
        }
        return sequence.size();
    }
}
```
2)Binary Search(Optimal)  
Based on 1), we can optimize the search progress using binary search.  
**Complexity: Time O(nlogn), Space O(n).**  
```java
class Solution {
    public int binarySearch(ArrayList<Integer> sequence, int target){
        int low = 0, high = sequence.size() - 1;
        while(low < high){
            int mid = (high - low) / 2 + low;
            if(sequence.get(mid) > target && (mid == 0 || sequence.get(mid - 1) < target)
              || sequence.get(mid) == target){
                return mid;
            }
            else{
                if(sequence.get(mid) < target){
                    low = mid + 1;
                }
                else{
                    high = mid - 1;
                }
            }
        }
        return low;
    }
    public int lengthOfLIS(int[] nums) {
        if(nums == null || nums.length == 0){
            return 0;
        }
        ArrayList<Integer> sequence = new ArrayList<>();
        sequence.add(nums[0]);
        for(int i = 1; i < nums.length; i++){
            if(nums[i] > sequence.get(sequence.size() - 1)){
                sequence.add(nums[i]);
            }
            else{
                int pos = binarySearch(sequence, nums[i]);
                sequence.set(pos, nums[i]);
            }
        }
        return sequence.size();
    }
}
```
