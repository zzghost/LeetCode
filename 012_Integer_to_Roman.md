# Integer to Roman
Given an integer, convert it to a roman numeral.

Input is guaranteed to be within the range from 1 to 3999.
## Solution
Table method.  
```java
class Solution {
    public String intToRoman(int num) {
        StringBuilder sb = new StringBuilder();
        String[] T = {"", "M", "MM", "MMM"};
        String[] H = {"", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM"};
        String[] D = {"", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC"};
        String[] S = {"", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX"};
        sb.append(T[num / 1000]);
        num %= 1000;
        sb.append(H[num / 100]);
        num %= 100;
        sb.append(D[num / 10]);
        num %= 10;
        sb.append(S[num]);
        return sb.toString();
    }
}
```
