# Count and Say
## Description
The count-and-say sequence is the sequence of integers with the first five terms as following:

1.     1
2.     11
3.     21
4.     1211
5.     111221
1 is read off as "one 1" or 11.
11 is read off as "two 1s" or 21.
21 is read off as "one 2, then one 1" or 1211.
Given an integer n, generate the nth term of the count-and-say sequence.

Note: Each term of the sequence of integers will be represented as a string.

Example:
```
Input: 1
Output: "1"
Example 2:
```
```
Input: 4
Output: "1211"
```
## Solution
```java
class Solution {
    public String countAndSay(int n) {
        String start = "1";
        if(n == 1) return start;
        for(int i = 1; i < n; i++){
            StringBuilder sb = new StringBuilder();
            char curr = ' ';
            if(start.length() > 0)
                curr = start.charAt(0);
            int count = 1;
            for(int j = 1; j < start.length(); j++){
                if(curr != start.charAt(j)){
                    sb.append(count);
                    sb.append(curr);
                    curr = start.charAt(j);
                    count = 1;
                }
                else{
                    count++;
                }
            }
            sb.append(count);
            sb.append(curr);
            start = sb.toString();
        }
        return start;
    }
}
```
