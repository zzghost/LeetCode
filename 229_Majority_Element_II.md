# Majority Element II
## Description
Given an integer array of size n, find all elements that appear more than ⌊ n/3 ⌋ times. The algorithm should run in linear time and in O(1) space.

## Solution
[Boyer-Moore Majority Vote algorithm](https://gregable.com/2013/10/majority-vote-algorithm-find-majority.html)  
**Complexity: Time O(n), Space O(1).**
```java
class Solution {
    public List<Integer> majorityElement(int[] nums) {
        List<Integer> rst = new ArrayList<>();
        if(nums == null)
            return rst;
        int y = 0, z = 1, cy = 0, cz = 0;
        for(int num : nums){
            if(num == y)
                cy++;
            else if(num == z)
                cz++;
            else if(cy == 0){
                y = num;
                cy++;
            }
            else if(cz == 0){
                z = num;
                cz++;
            }
            else{
                cy--;
                cz--;
            }
        }
        cy = 0; cz = 0;
        for(int num : nums)
            if(num == y)
                cy++;
            else if(num == z)
                cz++;
        if(cy > nums.length / 3)
            rst.add(y);
        if(cz > nums.length / 3)
            rst.add(z);
        return rst;
    }
}
```
