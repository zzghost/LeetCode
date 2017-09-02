# Missing Number
## Description
Given an array containing *n* distinct numbers taken from `0, 1, 2, ..., n`, find the one that is missing from the array.  
**Note:**  
Your algorithm should run in linear runtime complexity. Could you implement it using only constant extra space complexity?  
## Example
> For example,
> Given *nums* = `[0, 1, 3]` return `2`. 
## Solution
1. Sum of all.  
Use the equation, however, when n is large, such as `214745647`, the equation will overflow.
Complexity: Time O(n), Space O(1)  
```java
public int missingNumber(int[] nums) {
    int sum = 0;
    for(int x : nums)
        sum += x;
    //Overflow: when nums.length is large.
    return ((nums.length + 1) * nums.length  - 2 * sum) / 2;
}
//Another solution will avoid overflow.
public int missingNumber(int[] nums){
    int sum = 0;
    for(int i = 0; i < nums.length; i++)
        sum += (i + 1) - nums[i];
    return sum;
}
```
2. Swapping.  
Traversal pointer is *i*. It promises `nums[i] = i`. If not, exchange until the equation works.  
The situation `nums[i]==nums.length` must be taken into consideration. Actually, this number will finally on the missing number's position.  
Complexity: Time O(n), Space O(1)  
```java
public void Swap(int idx, int[] nums){
    while(idx != nums[idx])
        //Beware of nums[idx]=nums.length
        if(nums[idx] != nums.length){
            int tmp = nums[nums[idx]];
            nums[nums[idx]] = nums[idx];
            nums[idx] = tmp;
        }
        else return ;
}
public int missingNumber(int[] nums) {
    for(int i = 0; i < nums.length; i++){
        Swap(i, nums);
    }
    for(int i = 0; i < nums.length; i++)
        if(nums[i] != i)
            return i;
    return nums.length;
}
```
3. XOR.  
`X ^ X = 0, X ^ 0 = X.`
The index of array is 0...n-1, while number is 0...n.  
When we do all of the `nums[i] ^ i`, we get the missing number.  
Remember that the init value of rst must be nums.length as index doesn't have this value.  
Complexity: Time O(n), Space O(1).  
```java
public int missingNumber(int[] nums) {
    int rst = nums.length;
    for(int i = 0; i < nums.length; i++){
        rst = rst ^ nums[i] ^ i;
    }
    return rst;
}
```
