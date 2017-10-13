# Length of Last Word
## Description
Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string.  

If the last word does not exist, return 0.  

Note: A word is defined as a character sequence consists of non-space characters only.  

For example,  
Given s = "Hello World",  
return 5.  
## Solution
Start from end of the String.  
But trim the String first in case that it has lots of ' ' in the back.  
**Complexity: Time O(n), Space O(n).**
```java
public int lengthOfLastWord(String s) {
    if(s == null || s.length() == 0)
        return 0;
    int n = s.length();
    char[] alpha = s.toCharArray();
    int i = n - 1;
    while(i >= 0 && alpha[i] == ' ')
        i--;
    int start = i;
    for(; i >= 0; i--){
        if(alpha[i] == ' ')
            break;
    }
    return start - i;
}
```
