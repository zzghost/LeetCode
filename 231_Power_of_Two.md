# Power of Two
Given an integer, write a function to determine if it is a power of two.
## Solution
```java
class Solution {
    public boolean isPowerOfTwo(int n) {
        if(n <= 0) return false;
        int count = 0;
        while(n != 0){
            count += (n & 1);
            n >>>= 1;
        }
        return (count == 1);
    }
}
```

```java
class Solution {
    public boolean isPowerOfTwo(int n) {
        if(n <= 0) return false;
        return ( (n&(n - 1)) == 0);
    }
}
```
