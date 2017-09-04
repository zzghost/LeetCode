# K-diff Pairs in an Array
## Description
Given an array of integers and an integer k, you need to find the number of unique k-diff pairs in the array. Here a k-diff pair is defined as an integer pair (i, j), where i and j are both numbers in the array and their absolute difference is k.  
## Example
**Example 1:**  
```
Input: [3, 1, 4, 1, 5], k = 2  
Output: 2  
Explanation: There are two 2-diff pairs in the array, (1, 3) and (3, 5).  
Although we have two 1s in the input, we should only return the number of unique pairs.  
```
**Example 2:**  
```
Input:[1, 2, 3, 4, 5], k = 1  
Output: 4  
Explanation: There are four 1-diff pairs in the array, (1, 2), (2, 3), (3, 4) and (4, 5).  
```
**Example 3:**  
```
Input: [1, 3, 1, 5, 4], k = 0  
Output: 1  
Explanation: There is one 0-diff pair in the array, (1, 1).  
```
**Note:**  
1. The pairs (i, j) and (j, i) count as the same pair.  
2. The length of the array won't exceed 10,000.  
3. All the integers in the given input belong to the range: [-1e7, 1e7].  

1. Brute-Force. (Time Limit Exceeded).  
Complexity: Time O(n^2), Space O(n).  
```java
public int findPairs(int[] nums, int k) {
    Map<Integer, Integer> map = new HashMap<Integer, Integer>();
    for(int i = 0; i < nums.length; i++){
        for(int j = i + 1; j < nums.length; j++){
            if(Math.abs(nums[i] - nums[j]) == k){
                int key = Math.min(nums[i], nums[j]), value = Math.max(nums[i], nums[j]);
                if(!map.containsKey(key)){
                    map.put(key, value);
                }
            }
        }
    }
    return map.size();
}
```
2. Two-pointers.  
Firstly, sort the array. It takes O(nlogn) time.  
Secondly, use 2 pointer `start` and `end` to traversal.  
**Complexity: Time O(nlogn), Space O(1)**  
```java
public int findPairs(int[] nums, int k) {
    if(nums == null || nums.length == 0)
        return 0;
    Arrays.sort(nums);

    int start = 0, end = 1, count = 0;
    while(start < nums.length && end < nums.length){
        if(start == end || nums[start] + k > nums[end])
            end++;
        else if(nums[start] + k < nums[end])
            start++;
        else{
            //nums[start] + k = nums[end]
            count++;
            start++;
            //in case duplicates
            while(start < nums.length && nums[start] == nums[start - 1])
                start++;
            //make sure start < end
            end = Math.max(start + 1, end + 1);
        }
    }
    return count;
}
```
