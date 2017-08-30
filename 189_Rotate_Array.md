# Rotate Array
## Description
Rotate an array of n elements to the right by k steps.  
## Example
> For example, with n = 7 and k = 3, the array `[1,2,3,4,5,6,7]` is rotated to `[5,6,7,1,2,3,4]`. 
## Solution
1. Using Reverse.  
Based on the fact that when we rotate the array k times, k elements from the back end of the array come to the front and the rest of the elements from the front shift backwards.  
We firstly reverse all the elements of the array. Then, reversing the first k elements followed by reversing the rest *n-k* elements.  
Complexity: Time O(n), Space O(1).
```java
public void Reverse(int[] nums, int start, int end){
    if(start < end && end < nums.length && start >= 0){
        for(int i = start; i <= (start + end) / 2; i++){
            int tmp = nums[i];
            nums[i] = nums[end + start - i];
            nums[end + start - i] = tmp;
        }
    }
}
public void rotate(int[] nums, int k) {
    if(nums == null)
        return;
    k = k % nums.length;
    Reverse(nums, 0, nums.length - 1);
    Reverse(nums, 0, k - 1);
    Reverse(nums, k, nums.length - 1);
}
```
2. Using Extra Array  
Use extra array to place every element of the array at its correct position.  
index = (i + k) % length
Complexity: Time O(n), Space O(n)
```java
public void rotate(int[] nums, int k) {
    if(nums == null) return;
    k = k % nums.length;
    int[] rst = new int[nums.length];
    for(int i = 0; i < nums.length; i++)
        rst[(i + k) % nums.length] = nums[i];
    for(int i = 0; i < nums.length; i++)
        nums[i] = rst[i];
}
```
3. Using Cyclic Replacements.  
We directly place every number of the array at its required correct position.  
To avoid destroying the original element, we need to store the number being replaced in a *tmp* variable.  
Then we can place the number[*tmp*] at its correct position and so on, n times,where n is the length of the array.  
```java
public void rotate(int[] nums, int k) {
    if(nums == null) return;
    k = k % nums.length;
    int count = 0;
    for(int i = 0; count < nums.length; i++){
        int current = i;
        int currNum = nums[current];
        do{
            int next = (current + k) % nums.length;
            int tmp = nums[next];
            nums[next] = currNum;
            current = next;
            currNum = tmp;
            count++;
        }while(i != current);
    }
}
```
