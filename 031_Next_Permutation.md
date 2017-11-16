# Next Permutation
## Description
Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

The replacement must be in-place, do not allocate extra memory.

Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.  
`1,2,3` → `1,3,2`  
`3,2,1` → `1,2,3`  
`1,1,5` → `1,5,1`  

## Solution
**Complexity: Time O(n), Space O(1).**
```java
class Solution {
    public void swap(int[] nums,int i, int j){
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
    public void reverse(int[] nums, int i, int j){
        while(i < j)
            swap(nums, i++, j--);
    }
    public void nextPermutation(int[] nums) {
        int i = nums.length - 2;
        //find the first element x that breaks the descending order
        while(i >= 0 && nums[i] >= nums[i + 1])
            i--;
        //swap the first element which is larger than x and swap
        if(i >= 0){
            int j = nums.length - 1;
            while(nums[j] <= nums[i])
                j--;
            swap(nums, i, j);
        }
        //reverse the descending order array
        reverse(nums, i + 1, nums.length - 1);
    }
}
```
