# Plus One  
## Description  
Given a non-negative integer represented as a non-empty array of digits, plus one to the integer.  
You may assume the integer do not contain any leading zero, except the number 0 itself.  
The digits are stored such that the most significant digit is at the head of the list.  
##Example  
> array = [1,2,3,4]  
> output = [1,2,3,5]
## Solution  
Basic traversal.  
We can use one variable called carry to simulate the plus procedure.  
Take care that if all numbers in array are 9, we need to new an array,whose first item is 1 and others are zero.  
Here gives a simple solution.No need to use carry or check if all the number are 9.
```java
public int[] plusOne(int[] digits) {
    for(int i = digits.length - 1; i >= 0; i--){
        if(digits[i] < 9){
            digits[i]++;
            return digits;
        }
        digits[i] = 0;
    }
    int[] rst = new int[digits.length + 1];
    rst[0] = 1;
    return rst;
}
```
