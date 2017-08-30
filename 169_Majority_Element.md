# Majority Element 
## Description
Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.  
You may assume that the array is non-empty and the majority element always exist in the array.
## Solution
1. Sorting  
Complexity: Time O(nlogn), Space O(1)  
```java
public int majorityElement(int[] nums) {
    Arrays.sort(nums);
    return nums[nums.length / 2];
}
```
2. HashMap  
Key is nums[i], value is its appear time.  
Complexity: Time O(n), Space O(1)  
```java
public int majorityElement(int[] nums) {
    HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
    for(int i = 0; i < nums.length; i++){
        if(map.containsKey(nums[i]))
            map.put(nums[i], map.get(nums[i]) + 1);
        else
            map.put(nums[i], 1);
        if(map.get(nums[i]) > nums.length / 2)
            return nums[i];
    }
    return 0;
}
```
3. Moore voting algorithm  
Choose a candidate.  
If current number is same as candidate, vote positive;else, vote negtive.  
If count of the candidate is 0, it means pre-subarray has no half-appeared number.  
Complexity: Time O(n), Space O(1)
```java
public int majorityElement(int[] nums) {
    int count = 1, ret = nums[0];
    for(int i = 1; i < nums.length; i++){
        if(count == 0)
            ret = nums[i];
        if(ret == nums[i])
            count++;
        else
            count--;
    }
    return ret;
}
```
4. Bit manipulation  
Use bit to record the appear times.  
Complexity: Time O(n), Space O(1)
```java
public int majorityElement(int[] nums) {
    int[] bits = new int[32];
    for(int x : nums){
        for(int i = 0; i < 32; i++){
            if((x >> (31 - i) & 1) == 1)
                bits[i]++;
        }
    }
    int ret = 0;
    for(int i = 0; i < 32; i++){
        bits[i] = (bits[i] > nums.length / 2)? 1 : 0;
        ret += bits[i] * (1 << (31 - i));
    }
    return ret;
}
```
5. Parition-based algorithm  
It is based upon quik sort algorithm.  
The `partition()`function is to sort. If the returned idx is nums.length/2, it means after sorted, the num on this position is the wanted value.  
Complexity: Time O(n), Space O(1)  
```java
public int partition(int[] nums, int start, int end){
    int first = nums[start];
    while(start < end){
        while(start < end && nums[end] > first) end--;
        if(start < end)
            nums[start++] = nums[end];
        while(start < end && nums[start] < first) start++;
        if(start < end)
            nums[end--] = nums[start];
    }
    nums[start] = first;
    return start;
}
public int majorityElement(int[] nums) {
    int mid = nums.length >> 1, start = 0, end = nums.length - 1;
    int idx = partition(nums, start, end);
    while(idx != mid){
        if(idx > mid)
            end = idx - 1;
        else
            start = idx + 1;
        idx = partition(nums, start, end);
    }
    return nums[idx];
}
```
