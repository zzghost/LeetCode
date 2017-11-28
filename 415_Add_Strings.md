# Add Strings
## Description
Given two non-negative integers num1 and num2 represented as string, return the sum of num1 and num2.

**Note:**  

1. The length of both num1 and num2 is < 5100.
2. Both num1 and num2 contains only digits 0-9.
3. Both num1 and num2 does not contain any leading zero.
4. You must not use any built-in BigInteger library or convert the inputs to integer directly.

## Solution
```java
class Solution {
    public String addStrings(String num1, String num2) {
        int m = num1.length(), n = num2.length();
        int i = m - 1, j = n - 1, carry = 0;
        StringBuilder sb = new StringBuilder();
        while(i >= 0 || j >= 0){
            int sum = carry;
            if(j >= 0) sum += num2.charAt(j--) - '0';
            if(i >= 0) sum += num1.charAt(i--) - '0';
            carry = sum / 10;
            sum = sum % 10;
            sb.append(sum);
        }
        if(carry != 0)
            sb.append(carry);
        return sb.reverse().toString();
    }
}
```
