# Valid Triangle Number
## Description
Given an array consists of non-negative integers, your task is to count the number of triplets chosen from the array that can make triangles if we take them as side lengths of a triangle.  
## Example
```
Input: [2,2,3,4]  
Output: 3  
Explanation:  
Valid combinations are:  
2,3,4 (using the first 2)  
2,3,4 (using the second 2)  
2,2,3  
```
**Note:**  
1. The length of the given array won't exceed 1000.  
2. The integers in the given array are in the range of [0, 1000].  
## Solution
1. Three pointers.  
First, sort the array.  
`nums[i]` is the base.  
`nums[left]` is the smaller.  
`nums[right]` is the larger.  
if `nums[i] < nums[left] + nums[right]`, all numbers between `left` and `right - 1` can be the smaller edge. Then `right` go left.  
else, the smaller edge should go right to be larger.  
**Complexity: Time O(n^2), Space O(1)**
```java
public int triangleNumber(int[] nums) {
    int count = 0;
    if(nums.length < 3)
        return count;

    Arrays.sort(nums);

    for(int i = 2; i < nums.length; i++){
        int left = 0, right = i - 1;
        while(left < right){
            if(nums[left] + nums[right] > nums[i]){
            //all num larger than nums[left] form a triangle.
                count += right - left;
                right--;
            }
            //smaller number should be larger.
            else
                left++;
        }
    }
    return count;
}
```
