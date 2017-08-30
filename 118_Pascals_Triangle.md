# Pascal's Triangle
## Description
Given numRows, generate the first numRows of Pascal's triangle.  
## Example
> Given numRows = 5,  
> Return [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]  
## Solution
Dynamic Programming.  
Record the pre-row.  
Complexity: Time O(n^2), Space O(n)  
```java
public List<List<Integer>> generate(int numRows){
    List<List<Integer>> triangle = new ArrayList<List<Integer>>();
    if(numRows == 0)
        return triangle;
    List<Integer> row, pre = null;
    for(int i = 0; i < numRows; i++){
        row = new ArrayList<Integer>();
        for(int j = 0; j < i + 1; j++){
            if(j == 0 || j == i)
                row.add(1);
            else
                row.add(pre.get(j-1) + pre.get(j));
        }
        triangle.add(row);
        pre = row;
    }
    return triangle;
}
```
