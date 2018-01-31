# Happy Number
Write an algorithm to determine if a number is "happy".

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

Example: 19 is a happy number
```
1^2 + 9^2 = 82
8^2 + 2^2 = 68
6^2 + 8^2 = 100
1^2 + 0^2 + 0^2 = 1
```
## Solution
```java
class Solution {
    public boolean isHappy(int n) {
        Set<Integer> set = new HashSet<>();
        while(n != 1){
            int sum = 0;
            int tmp = n;
            while(tmp != 0){
                sum += Math.pow(tmp % 10, 2);
                tmp /= 10;
            }
            if(set.contains(sum))
                return false;
            else
                set.add(sum);
            n = sum;
        }
        return true;
    }
}
```
