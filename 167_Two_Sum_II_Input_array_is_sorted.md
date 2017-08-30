# Two Sum II - Input array is sorted
## Descrition
Given an array of integers that is already **sorted in ascending order**, find two numbers such that they add up to a specific target number.  
The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.  
You may assume that each input would have *exactly* one solution and you may not use the same element twice.
## Example
> Input: numbers={2, 7, 11, 15}, target=9  
> Output: index1=1, index2=2  
## Solution
Two pointers:low and high to denote the first index and second index respectively.  
We should notice that this array is sorted.  
Complexity: Time O(n), Space O(1).  
Besides we can use binary search to do the less efficient search.  
```java
public int[] twoSum(int[] numbers, int target) {
    if(numbers == null || numbers.length == 0) return null;
    int low = 0, high = numbers.length - 1;
    while(low < high){
        int sum = numbers[low] + numbers[high];
        if(sum == target)
            return new int[]{low+1, high+1};
        else if(sum > target)
            high--;
        else
            low++;
    }
    throw new IllegalArgumentException("No two solutions.");
}
```
