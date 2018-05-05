# ZigZag Conversion
The string ``"PAYPALISHIRING"`` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)
```
P   A   H   N
A P L S I I G
Y   I   R
```
And then read line by line: ``"PAHNAPLSIIGYIR"``
Write the code that will take a string and make this conversion given a number of rows:

string convert(string text, int nRows);
``convert("PAYPALISHIRING", 3)`` should return ``"PAHNAPLSIIGYIR"``.

## Solution
Math.  
Count each position's index.   
Each line's loop is `2 * numRows - 2`,
```java
class Solution {
    public String convert(String s, int numRows) {
        if(s == null || s.length() <= numRows) return s;
        //c is the loop, gap is the zigzag's gap, row counts each line.
        int c = 2 * numRows - 2, row = 0, gap = 0, n = s.length();
        if(c <= 0) return s;
        StringBuilder sb = new StringBuilder();
        while(row < numRows){
            int pos = row;
            while(pos - gap < n || pos < n){
              //record the zigzag's num,gap=0 is the first line, gap=c is the last line
                if(gap != 0 && pos > gap && gap < c)
                    sb.append(s.charAt(pos - gap));
              //record the line's  num
                if(pos < n)
                    sb.append(s.charAt(pos));
                pos += c;
            }
            gap += 2;
            row++;
        }
        return sb.toString();
    }
}
```
