# Valid Perfect Square
## Description
Given a positive integer num, write a function which returns True if num is a perfect square else False.  

Note: Do not use any built-in library function such as sqrt.  
## Example
**Example 1:**  
```
Input: 16
Returns: True
```
**Example 2:**  
```
Input: 14
Returns: False
```
## Solution
**Complexity: Time O(logn), Space O(1)**  
```java
public boolean isPerfectSquare(int num) {
//take care of overflow.
    long low = 1, high = num;
    while(low < high){
        long mid = (high - low) / 2 + low;
        long square = mid * mid;
        if(square == num){
            return true;
        }
        if(square < num)
            low = mid + 1;
        else
            high = mid - 1;   
    }
    if(low * low == num)
        return true;
    return false;
}
```
