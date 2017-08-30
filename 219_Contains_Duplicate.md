# Contains Duplicate II
## Description
Given an array of integers and an integer k, find out whether there are two distinct indices i and j in the array such that nums[i] = nums[j] and the absolute difference between i and j is at most k.  
## Solution
Use hashmap, key: num, value: index.  
Complexity: Time O(n), Space O(n)
```java
public boolean containsNearbyDuplicate(int[] nums, int k) {
    if(nums == null || nums.length == 0) return false;
    int len = nums.length;
    HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
    for(int i = 0; i < len; i++){
        if(map.containsKey(nums[i])){
            int idx = map.get(nums[i]);
            if(i - idx <= k)
                return true;
        }
        map.put(nums[i], i);
    }
    return false;
}
```
