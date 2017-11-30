# Palindrome Number
## Description
Determine whether an integer is a palindrome. Do this without extra space.
## Solution
**Complexity: Time O(logn), Space O(n)**
```java
class Solution {
    public boolean isPalindrome(int x) {
        if(x < 0) return false;
        int p = x, q = 0;
        while(p != 0){
            q *= 10;
            q += p % 10;
            p /= 10;
        }
        return q == x;
    }
}
```
