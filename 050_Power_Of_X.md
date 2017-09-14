# Pow(x,n)
## Description
Implement pow(x, n).  
## Solution
Both are based upon 
1. Recursive/Divide and Conquer.  
**Complexity: Time O(logn), Space O(logn)**  
```java
public double pow(double x, long n){
    if(n == 0)
        return 1;
    if(n == 1)
        return x;
    double result = pow(x, n / 2);
    result *= result;
    if(n % 2 != 0)
        result *= x;
    return result;
}
public double myPow(double x, int n) {
    if(x == 0 || n == 1)
        return x;
    if(n == 0 || x == 1)
        return 1;
    //when n is Integer.MAX_VALUE, Math.abs(N) will overflow.
    long N = n;
    double result = pow(x, Math.abs(N));

    if(N < 0)
        result = 1.0 / result;
    return result;

}
```
2. Bit manipulation.  
**Complexity: Time O(logn), Space O(1)**
```java
public double myPow(double x, int n) {
    if(x == 0 || n == 1)
        return x;
    if(n == 0 || x == 1)
        return 1;
    long N = Math.abs((long) n);
    double rst = 1;
    while(N != 0){
        if((N&1) == 1) rst *= x;
        x *= x;
        N >>= 1;
    }
    return (n > 0) ? rst : 1.0/rst;
}
```
