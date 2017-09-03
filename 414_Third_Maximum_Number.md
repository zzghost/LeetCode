# Third Maximum Number  
## Description  
Given a non-empty array of integers, return the third maximum number in this array. If it does not exist, return the maximum number. The time complexity must be in O(n).  
## Example  
**Example 1:**  
```
Input: [3, 2, 1]  

Output: 1  

Explanation: The third maximum is 1.  
```
**Example 2:**  
```
Input: [1, 2]  

Output: 2  

Explanation: The third maximum does not exist, so the maximum (2) is returned instead.  
```
**Example 3:**  
```
Input: [2, 2, 3, 1]  

Output: 1  

Explanation: Note that the third maximum here means the third maximum distinct number.  
Both numbers with value 2 are both considered as second maximum.  
```
## Solution
1. TreeSet.  
TreeSet allows no duplicate and is sorted.  
Complexity: Time O(logn), Space O(logn)  
```java
public int thirdMax(int[] nums) {
    TreeSet<Integer> set = new TreeSet<Integer>();
    for(int x : nums)
        set.add(x);
    if(set.size() >= 3){
        set.pollLast();
        set.pollLast();
        return set.pollLast();
    }
    else
        return set.pollLast();
}
```
2. Singal Scan.(Optimal)
Since numbers can be Integer.MIN_VALUE in `nums`, we use `Integer` instead of `int`.  
`Integer` inital value is null which is convenient for the recognition of changing variable `max3`.  
Complexity: Time O(n), Space O(1)  
```java
public int thirdMax(int[] nums) {
    Integer max1, max2, max3;
    max1 = max2 = max3 = null;
    for(Integer x : nums){
        if(x.equals(max1) || x.equals(max2) || x.equals(max3)) continue;
        if(max1 == null || x > max1){
            max3 = max2;
            max2 = max1;
            max1 = x;
        }
        else if(max2 == null || x > max2){
            max3 = max2;
            max2 = x;
        }
        else if(max3 == null || x > max3){
            max3 = x;
        } 
    }
    return (max3 != null) ? max3 : max1;
}
```
