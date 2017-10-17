# Combination SumIII
Related problemns: [039_Combination_Sum](https://github.com/zzghost/leetcode/blob/master/039_Combination_Sum.md), [040 Combination SumII](https://github.com/zzghost/leetcode/blob/master/040_Combination_Sum_II.md)  
## Description
Find all possible combinations of k numbers that add up to a number n, given that only numbers from 1 to 9 can be used and each combination should be a unique set of numbers.

Example 1:
```
Input: k = 3, n = 7

Output:

[[1,2,4]]
```
Example 2:
```
Input: k = 3, n = 9

Output:

[[1,2,6], [1,3,5], [2,3,4]]
```
## Solution
Backtracking.  
**Complexity: Time O(2^n).**
```java
class Solution {
    List<List<Integer>> list = new ArrayList<>();
    List<Integer> aList = new ArrayList<>();
    public void find(int k, int n, int idx){
        if(n == 0 && aList.size() == k){
            list.add(new ArrayList<>(aList));
            return ;
        }
        if(n < 0 || idx > 9)
            return ;
        for(int i = idx; i <= 9; i++){
            aList.add(i);
            find(k, n - i, i + 1);
            aList.remove(aList.size() - 1);
        }
    }
    public List<List<Integer>> combinationSum3(int k, int n) {
        find(k, n, 1);
        return list;
    }
}
```
