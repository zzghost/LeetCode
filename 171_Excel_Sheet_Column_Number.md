# Excel Sheet Column Number
## Description

Related to question [Excel Sheet Column Title](https://leetcode.com/problems/excel-sheet-column-title/description/)

Given a column title as appear in an Excel sheet, return its corresponding column number.

For example:

    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28

## Solution
```java
class Solution {
    public int titleToNumber(String s) {
        if(s == null || s.length() == 0){
            return 0;
        }
        int n = s.length();
        int rst = 0;
        for(int i = 0; i < n; i++){
            char c = s.charAt(i);
            rst = rst * 26 + (c - 'A' + 1);
        }
        return rst;
    }
}
```
