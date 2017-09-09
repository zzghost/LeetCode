# Beautiful Arrangement
## Description
Suppose you have N integers from 1 to N. We define a beautiful arrangement as an array that is constructed by these N numbers successfully if one of the following is true for the ith position (1 <= i <= N) in this array:  

1. The number at the ith position is divisible by i.  
2. i is divisible by the number at the ith position.  
Now given N, how many beautiful arrangements can you construct?  
## Example
**Example 1:**  
```
Input: 2  
Output: 2  
Explanation:  

The first beautiful arrangement is [1, 2]:  

Number at the 1st position (i=1) is 1, and 1 is divisible by i (i=1).  

Number at the 2nd position (i=2) is 2, and 2 is divisible by i (i=2).  

The second beautiful arrangement is [2, 1]:  

Number at the 1st position (i=1) is 2, and 2 is divisible by i (i=1).  

Number at the 2nd position (i=2) is 1, and i (i=2) is divisible by 1.  
```
**Note:**  
1. N is a positive integer and will not exceed 15.  


## Solution
Backtracking.
**Complexity: Time O(k), Space O(n). k refers to the number of valid permutation.**
```java
public int count = 0;

public void arrange(int[] numTaken, int position, int N){
    //All numbers have been put.
    if(position > N){
        count++;
        return ;
    }

    for(int i = 0; i < N; i++){
        if(numTaken[i] != 1 && ((i + 1) % position == 0 || position % (i + 1) == 0)){
            numTaken[i] = 1;
            arrange(numTaken, position + 1, N);
            numTaken[i] = 0;
        }
    }
}

public int countArrangement(int N) {
    int[] numTaken = new int[N];
    arrange(numTaken, 1, N);
    return count;
}
```
