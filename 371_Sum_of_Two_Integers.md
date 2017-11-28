# Sum of Two Integers
## Description
Calculate the sum of two integers a and b, but you are not allowed to use the operator + and -.

Example:
Given a = 1 and b = 2, return 3.
## Solution
Half-plus algorithm.  
Two bits use "^" to get the answer, use "&" to get the carry.  
e.g.:a = 11: 1011, b = 5: 0101.  
a & b: 0001 is the carry, we can see that last position has a carry.  
a ^ b: 1110 is the sum.
Then we add the carry(Right move one position) and the sum  
```java
class Solution {
    public int getSum(int a, int b) {
        if(a == 0) return b;
        if(b == 0) return a;
        while(b != 0){
            int carry = a & b;
            a = a ^ b;
            //let carry be b
            b = carry << 1;
        }
        return a;
    }
}
```
