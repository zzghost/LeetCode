# Count Primes
Count the number of prime numbers less than a non-negative number, n.
## Solution
Usually there is a data structure like `ArrayList` to save the prime, and then we enumerate from 2 to n to see if this number can be divided by the prime number.  
But this will TLE.  
Here comes another solution, which is a reverse-thinking.  
We start `i` from 2 to n, and mark the notPrime.  
```java
class Solution {
    public int countPrimes(int n) {
        if(n <= 1) return 0;
        boolean[] notPrime = new boolean[n];
        int count = 0;
        for(int i = 2; i < n; i++){
            if(notPrime[i] == false){
                count++;
                //the notPrime then will be skiped.
                for(int j = 2; i * j < n; j++)
                    notPrime[i * j] = true;
            }
        }
        return count;
    }
}
```
