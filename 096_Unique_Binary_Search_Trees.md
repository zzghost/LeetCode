# Unique Binary Search Trees
Given n, how many structurally unique BST's (binary search trees) that store values 1...n?

For example,
Given n = 3, there are a total of 5 unique BST's.
```
   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```
## Solution
1. Recursive.(TLE)  
nodes of left subtrees multiply nodes of right subtrees.  
```java
class Solution {
    public int numTrees(int n) {
        if(n <= 1) return 1;
        int sum = 0;
        for(int i = 1; i <= n; i++)
            sum += numTrees(i - 1) * numTrees(n - i);
        return sum;
    }
}
```
2. Dynamic Programming.  
array `num[i]` denotes the number of unique BST when `n = i`.  
```java
class Solution {
    public int numTrees(int n) {
        if(n <= 1) return 1;
        int[] num = new int[n + 1];
        num[0] = 1;
        num[1] = 1;
        for(int i = 2; i <= n; i++){
            int sum = 0;
            for(int j = 0; j <= i - 1; j++)
                sum += num[j] * num[i - j - 1];
            num[i] = sum;
        }

        return num[n];
    }
}
```
