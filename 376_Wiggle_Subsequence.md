# Wiggle Subsequence
A sequence of numbers is called a wiggle sequence if the differences between successive numbers strictly alternate between positive and negative. The first difference (if one exists) may be either positive or negative. A sequence with fewer than two elements is trivially a wiggle sequence.

For example, ``[1,7,4,9,2,5]`` is a wiggle sequence because the differences ``(6,-3,5,-7,3`)`` are alternately positive and negative. In contrast, ``[1,4,7,2,5]`` and ``[1,7,4,5,5]`` are not wiggle sequences, the first because its first two differences are positive and the second because its last difference is zero.

Given a sequence of integers, return the length of the longest subsequence that is a wiggle sequence. A subsequence is obtained by deleting some number of elements (eventually, also zero) from the original sequence, leaving the remaining elements in their original order.

**Examples:**  
```
Input: [1,7,4,9,2,5]
Output: 6
The entire sequence is a wiggle sequence.

Input: [1,17,5,10,13,15,10,5,16,8]
Output: 7
There are several subsequences that achieve this length. One is [1,17,10,13,10,16,8].

Input: [1,2,3,4,5,6,7,8,9]
Output: 2
```
**Follow up:**  
Can you do it in O(n) time?



## Solution
**Finit State Machine** and **Greedy**.  
Take `[1, 17, 5, 10, 13, 15, 10, 5, 16 ,8]` as an example.  
We take first 6 elments: `[1, 17, 5, 10, 13, 15]`.  
We can find that there are three subsequences `[1, 17, 5, 10]`, `[1, 17, 5, 13]`, `[1, 17, 5, 15]`.Which one should we pick?  
The truth is: we pick the max element `15` in order to get more following elements.(This is **Greedy**.)  
And then we find that there are three states: begin, up and down.  
In up state and down state: we pick the first and last elements, which means when the state changes, we pick the element.    
**Complexity: Time O(n), Space O(1).**  
```java
class Solution {
    public int wiggleMaxLength(int[] nums) {
        if(nums == null || nums.length == 0){
            return 0;
        }
        int n = nums.length, maxLength = 1;
        final int BEGIN = 0, UP = 1, DOWN = 2;
        int STATE = BEGIN;
        for(int i = 1; i < n; i++){
            switch(STATE){
                case BEGIN:{
                    if(nums[i - 1] < nums[i]){
                        STATE = UP;
                        maxLength++;
                    }
                    else if(nums[i - 1] > nums[i]){
                        STATE = DOWN;
                        maxLength++;
                    }
                    break;
                }
                case UP:{
                    if(nums[i - 1] > nums[i]){
                        STATE = DOWN;
                        maxLength++;
                    }
                    break;
                }
                case DOWN:{
                    if(nums[i - 1] < nums[i]){
                        STATE = UP;
                        maxLength++;
                    }
                    break;
                }
            }
        }
        return maxLength;

    }
}
```
