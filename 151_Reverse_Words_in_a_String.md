# Reverse Words in a String
Given an input string, reverse the string word by word.

For example,  
Given s = "the sky is blue",  
return "blue is sky the".  

Update (2015-02-12):  
For C programmers: Try to solve it in-place in O(1) space.

Clarification:
+ What constitutes a word?  
  A sequence of non-space characters constitutes a word.
+ Could the input string contain leading or trailing spaces?  
  Yes. However, your reversed string should not contain leading or trailing spaces.
+ How about multiple spaces between two words?  
  Reduce them to a single space in the reversed string.

## Solution
**Complexity: Time O(n^2), Space O(1).**
```java
public class Solution {
    public void reverse(char[] str, int start, int end){
        for(int i = start; i < (end - start) / 2 + start; i++){
                char tmp = str[i];
                str[i] = str[end + start - i - 1];
                str[end + start - i - 1] = tmp;
        }
    }
    public String reverseWords(String s) {
        //skip the spaces
        s = s.trim();
        int n = s.length();
        char[] str = s.toCharArray();
        //total reverse
        reverse(str, 0, n);
        int start = 0, end = start;
        while(start != n){
            start = end;
            while(end < n && str[end] != ' ') end++;
            reverse(str, start, end);
            //skip duplicate spaces
            while(end < n && str[end] == ' ') end++;
        }
        int count = 0, p = 0;
        for(int i = 0; i < n; ){
            if(str[i] != ' '){
                str[p++] = str[i++];
                count = 0;
            }
            else{
                if(count == 0)
                    str[p++] = str[i++];
                else
                    i++;
                count++;
            }
        }
        return new String(str).substring(0, p);
    }
}
```
