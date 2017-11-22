# Jump Game II
## Description
Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

For example:
Given array A = `[2,3,1,1,4]`

The minimum number of jumps to reach the last index is `2`. (Jump 1 step from index 0 to 1, then 3 steps to the last index.)

**Note:**  
You can assume that you can always reach the last index.
## Solution
Greedy.  
At each position, there's a jump interval like [start .. end], and in this interval, we pick the next start position.  
And the position `i` satisfies the condition: `max(nums[i] + j - end)`.It means that each jump, we pick the position that allows us to jump the longest distance.  
**Complexity: Time O(n), Space O(1).**
```java
class Solution{
  public int jump(int[] nums){
    if(nums == null || nums.length == 0 || nums.length == 1)
      return 0;
    int n = nums.length, last = nums[0], count = 1;
    for(int i = 0; i < n; ){
      last = nums[i] + i;
      if(last >= n - 1){  //reach the end
        break;
      }
      int max = 0, idx = i + 1;
      for(int j = i + 1; j <= last && j < n; j++){
        if(nums[j] + j - last >= max){
          max = nums[j] + j - last;
          idx = j;
        }
      }
      count++;
      i = idx;
    }
    return count;
  }
}
```
One more concise solution:
```java
class Solution{
  public int jump(int[] nums){
    int jumps = 0, curEnd = 0, curFarthest = 0;
    for(int i = 0; i < n; i++){
      curFarthest = Math.max(curFarthest, i + nums[i]);
      if(i == curEnd){
        jumps++;
        curEnd = curFarthest;
      }
    }
    return jumps;
  }
}
```
