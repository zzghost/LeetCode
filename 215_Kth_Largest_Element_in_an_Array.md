# Kth Largest Element in an Array
## Description
Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.
For example,
Given ``[3,2,1,5,6,4]`` and `k = 2`, return `5`.

Note:
You may assume k is always valid, 1 ≤ k ≤ array's length.
## Solution
**Complexity: Time O(nlogK), Space O(1).**  
```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        //size=k
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        for(int num : nums){
            if(pq.size() < k){
                pq.offer(num);
            }
            else if(pq.peek() < num){
                pq.poll();
                pq.offer(num);
            }
        }
        return pq.peek();
    }
}
```
