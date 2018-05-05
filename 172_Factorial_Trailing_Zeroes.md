# Factorial Trailing Zeroes
Given an integer n, return the number of trailing zeroes in n!.

**Note:** Your solution should be in logarithmic time complexity.  
## Solution
Because `0` is from `2*5`.  
And we found that when `n = 5` and `n!=(2*2*2*3*5)`,there's one `2*5`,
when `n =11` and `n!=(2^8*3^4*5^2*7)`,there's two `2*5`.  
It's obvious that there are more 2 than 5.So we only need to count the amount of `5`.  

```java
class Solution {
    public int trailingZeroes(int n) {
        return (n == 0) ? 0 : n / 5 + trailingZeroes(n / 5);
    }
}
```
