# Guess Number Higher or Lower
## Description
We are playing the Guess Game. The game is as follows:  

I pick a number from 1 to n. You have to guess which number I picked.  

Every time you guess wrong, I'll tell you whether the number is higher or lower.  

You call a pre-defined API guess(int num) which returns 3 possible results (-1, 1, or 0):  
```
-1 : My number is lower
 1 : My number is higher
0 : Congrats! You got it!
```
**Example:**  
```
n = 10, I pick 6.  

Return 6.
```
## Solution
**Complexity: Time O(logn), Space O(1)**
```java
public int guessNumber(int n) {
    int low = 1, high = n;
    while(low < high){
        int mid = (high - low) / 2 + low;

        int guessRst = guess(mid);
        if(guessRst == 0)
            return mid;
        if(guessRst == 1){
            low = mid + 1;
        }
        else
            high = mid;
    }
    return low;
}
```
