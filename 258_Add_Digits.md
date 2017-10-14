# Add Digits
## Description
Given a non-negative integer num, repeatedly add all its digits until the result has only one digit.  

For example:  

Given num = 38, the process is like: 3 + 8 = 11, 1 + 1 = 2. Since 2 has only one digit, return it.  

**Follow up:**
Could you do it without any loop/recursion in O(1) runtime?  
## Solution
1. Use loop
```java
public int addDigits(int num) {
    while(num/10 > 0){
        int sum = 0;
        while(num != 0){
            sum += (num % 10);
            num /= 10;
        }
        num = sum;
    }
    return num;
}
```
2. Digital root(O(1) runtime)
[See Wiki](https://en.wikipedia.org/wiki/Digital_root)
```java
public int addDigits(int num) {
    return num - 9 * ((num - 1) / 9);
}
```
