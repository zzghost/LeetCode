# Detect Capital
## Description
Given a word, you need to judge whether the usage of capitals in it is right or not.  

We define the usage of capitals in a word to be right when one of the following cases holds:  

All letters in this word are capitals, like "USA".  
All letters in this word are not capitals, like "leetcode".  
Only the first letter in this word is capital if it has more than one letter, like "Google".  
Otherwise, we define that this word doesn't use capitals in a right way.  
## Example
```
Example 1:
Input: "USA"
Output: True
Example 2:
Input: "FlaG"
Output: False
```
**Note:** The input will be a non-empty word consisting of uppercase and lowercase latin letters.  
## Solution
**Complexity: Time O(n), Space O(n)**
```java
public boolean detectCapitalUse(String word) {
    char[] alpha = word.toCharArray();
    int n = word.length();
    boolean upcase = false;
    for(int i = 1; i < n; i++){
    //example:gOogle
        if(alpha[0] >= 'a' && alpha[0] <= 'z')
            if(alpha[i] >= 'A' && alpha[i] <= 'Z')
                return false;
        if(alpha[0] >= 'A' && alpha[0] <= 'Z'){
    //example:FLag
            if(i > 1 && alpha[i] >= 'a' && alpha[i] <= 'z'){
                if(alpha[1] >= 'A' && alpha[1] <= 'Z')
                    return false;
            }
    //example:FlaG
            if(i > 1 && alpha[i] >= 'A' && alpha[i] <= 'Z'){
                if(alpha[1] >= 'a' && alpha[1] <= 'z')
                    return false;
            }
        }
    }
    return true;
}
```
