# Sqrt(x)
## Description
Implement `int sqrt(int x)`.  

Compute and return the square root of x.  

## Solution
**Complexity: Time O(logn), Space O(1).**  
```java
public boolean multiple(long num, long x){
    return (num * num <= x);
}
public int mySqrt(int x) {
    long start = 1, end = x;
    long rst = x;
    while(start < end){
        long mid = (end - start) / 2 + start;

        if(multiple(mid, x)){
            rst = mid;
            start = mid + 1;
        }
        else{
            end = mid;
        }
    }
    return (int)rst;
}
```
