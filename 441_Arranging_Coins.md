#Arranging Coins
## Description
You have a total of n coins that you want to form in a staircase shape, where every k-th row must have exactly k coins.  

Given n, find the total number of full staircase rows that can be formed.  

n is a non-negative integer and fits within the range of a 32-bit signed integer.  
## Example
**Example 1:**  
```
n = 5

The coins can form the following rows:
¤
¤ ¤
¤ ¤

Because the 3rd row is incomplete, we return 2.
```
**Example 2:**  
```
n = 8

The coins can form the following rows:
¤
¤ ¤
¤ ¤ ¤
¤ ¤

Because the 4th row is incomplete, we return 3.
```
## Solution
**Complexity: Time O(logn), Space O(1)**  
```java
public boolean canPut(long mid, int n){
    long rst = (1 + mid) * mid / 2;
    return (rst <= n);
}
public int arrangeCoins(int n) {
//take care of overflow.
    long low = 1, high = n, row;
    row = (low <= n) ? low : 0;
    while(low < high){
        long mid = (high - low) / 2 + low;

        if(canPut(mid, n)){
            row = mid;
            low = mid + 1;
        }
        else
            high = mid;
    }
    return (int)row;
}
```
