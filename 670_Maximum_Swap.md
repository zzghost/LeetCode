# Maximum Swap
## Description
Given a non-negative integer, you could swap two digits at most once to get the maximum valued number. Return the maximum valued number you could get.
```
Example 1:
Input: 2736
Output: 7236
Explanation: Swap the number 2 and the number 7.
Example 2:
Input: 9973
Output: 9973
Explanation: No swap.
```
Note:  
The given number is in the range [0, 108]
## Solution
Greedy.  
Higher position should have larger number.So each position we find the max number, if it's not the max number, then swap.  
**Complexity: O(n^2), O(n).**
```java
class Solution {
    public int findMaxIndex(int[] nums, int idx){
        int max = idx;
        for(int i = idx - 1; i >= 0; i--){
            if(nums[i] >= nums[max])
                max = i;
        }
        return max;
    }
    public int maximumSwap(int num) {
        int[] nums = new int[8];
        int n = num, size = 0;
        while(n != 0){
            nums[size++] = n % 10;
            n /= 10;
        }
        for(int i = size - 1; i >= 0; i--){
            int idx = findMaxIndex(nums, i);
            if(idx == i || nums[idx] == nums[i])
                continue ;
            else{
                int tmp = nums[idx];
                nums[idx] = nums[i];
                nums[i] = tmp;
                break;
            }
        }
        int rst = 0;
        for(int i = size - 1; i >= 0; i--)
            rst = rst * 10 + nums[i];
        return rst;
    }
}
```
