# Summary Ranges
## Description
Given a sorted integer array without duplicates, return the summary of its ranges.

Example 1:
```
Input: [0,1,2,4,5,7]
Output: ["0->2","4->5","7"]
```
Example 2:
```
Input: [0,2,3,4,6,8,9]
Output: ["0","2->4","6","8->9"]
```
## Solution
Traversal.
**Complexity: Time O(n), Space O(n)**
```java
class Solution {
    public List<String> summaryRanges(int[] nums) {
        List<String> rst = new ArrayList<>();
        if(nums == null || nums.length == 0)
            return rst;
        int i = 0;
        while(i < nums.length){
            int start = i;
            while(i < nums.length - 1 && nums[i] + 1 == nums[i + 1])
                i++;
            if(start != i)
                rst.add(String.valueOf(nums[start] + "->" + nums[i]));
            else
                rst.add(String.valueOf(nums[start]));
            i++;
        }
        return rst;
    }
}
```
