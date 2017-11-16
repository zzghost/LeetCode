# Longest Consecutive Sequence
## Description
Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

For example,
Given `[100, 4, 200, 1, 3, 2]`,
The longest consecutive elements sequence is `[1, 2, 3, 4]`. Return its length: `4`.

Your algorithm should run in O(n) complexity.
## Solution
Use *Set*.  
**Complexity: Time O(n), Space O(n).**
```java
class Solution {
    public int longestConsecutive(int[] nums) {
        if(nums == null || nums.length == 0)
            return 0;
        Set<Integer> set = new TreeSet<>();
        for(int x : nums)
            set.add(x);
        int count = 1, max = 1;
        Iterator iter = set.iterator();
        int x = 0, y = 0;
        if(iter.hasNext())
            x = (int)iter.next();
        while(iter.hasNext()){
            y = (int)iter.next();
            if(x + 1 == y){
                count++;
            }
            else{
                max = Math.max(count, max);
                count = 1;
            }
            x = y;
        }
        max = Math.max(count, max);
        return max;
    }
}
```
