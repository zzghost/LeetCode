# Single Number II

## Solution
Bit Manipulation.
1. Use a number to record appearance of each bits.If the bit appears less than 3 times, it's a bit in the result number.  
```java
class Solution {
    public int singleNumber(int[] nums) {
        int rst = 0;
        for(int i = 0; i < 32; i++){
            int sum = 0;
            //sum the number by bit
            for(int j = 0; j < nums.length; j++){
                sum += (nums[j] >> i) & 1;
            }
            //add to the result
            rst = rst | ((sum % 3) << i);
        }
        return rst;
    }
}
```
2. Use three variables.  
`one`, `two`, `three` to count each number's appearance, finally return `one` denoting the number appears only one time.  
If `nums[i]` appears once, update `one = one ^ nums[i]`.  
If `nums[i]` appears  twice, update `two = (one & nums[i]) | two`.  
If `nums[i]` appears three times, update `three = one & two` and update `one` and `two` again.  
```java
class Solution {
    public int singleNumber(int[] nums) {
        int one = 0, two = 0, three = 0;
        for(int num : nums){
            two = two | num & one;
            one = one ^ num;
            three = one & two;
            one = one & ~three;
            two = two & ~three;
        }
        return one;
    }
}
```
