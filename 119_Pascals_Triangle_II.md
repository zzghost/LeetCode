# Pascal's Triangle II 
## Description
Given an index k, return the kth row of the Pascal's triangle.  
**Note:**  
Could you optimize your algorithm to use only O(k) extra space?  
## Example
> For example, given k = 3,  
> Return `[1,3,3,1]`. 
## Solution
Dynamic Programming.  
Same as `118, Pascal's Triangle`. Here's a nice solution, which only use one variable.  
Complexity: Time O(n), Space O(n).
```java
public List<Integer> getRow(int rowIndex) {
    List<Integer> row = new ArrayList<Integer>();
    for(int i = 0; i <= rowIndex; i++){
        row.add(1);
        for(int j = i-1; j > 0; j--)
            row.set(j, row.get(j - 1) + row.get(j));
    }
    return row;
}
```
