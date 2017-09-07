# Find the Duplicate Number 
Given an array nums containing n + 1 integers where each integer is between 1 and n (inclusive), prove that at least one duplicate number must exist. Assume that there is only one duplicate number, find the duplicate one.  

**Note:**  

1. You must not modify the array (assume the array is read only).  
2. You must use only constant, O(1) extra space.  
3. Your runtime complexity should be less than O(n2).  
4. There is only one duplicate number in the array, but it could be repeated more than once.  

## Solution
`Tortoise and Hare algorithm` for cycle detection.  
We view the array as a linked list, each index points to the value. Each integer is between 1 and n and the index is ranging from 0 to n-1. Thus we need to subtract 1 from the array.  
Actually, we can minus one when we do traversal instead of modifying the array.  
Now we turn the problem into a `find common listnode in a cyclic linkedlist`.  
First, two pointers: fast and slow. Make fast pointer go 2 steps and slow pointer 1 step at a time. They will meet inside the cycle.  
Second, make `slow=n` and they go 1 step at the same time. They will stop at the idx which points to the same value.  

**Complexity: Time O(n), Space O(1)**  

Plus:  
We can make slow and fast starts at 0, and then we do not need to do array deduction.  
```java
public int findDuplicate(int[] nums) {
    int n = nums.length;
    int slow = n, fast = n;
    do{
        slow = nums[slow - 1];
        fast = nums[nums[fast - 1] - 1];
    }while(slow != fast);
    slow = n;
    while(slow != fast){
        slow = nums[slow - 1];
        fast = nums[fast - 1];
    }
    return slow;
}
```
