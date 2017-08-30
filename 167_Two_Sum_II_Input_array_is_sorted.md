# Two Sum II - Input array is sorted
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
