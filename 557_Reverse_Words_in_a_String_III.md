#Reverse Words in a String III
## Description
Given a string, you need to reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.  

##Example
```
Input: "Let's take LeetCode contest"
Output: "s'teL ekat edoCteeL tsetnoc"
```
**Note:** In the string, each word is separated by single space and there will not be any extra space in the string.  

## Solution
**Complexity: Time O(n^2), Space O(n).** 
```java
public void reverse(char[] alpha, int start, int end){
    for(int i = start; i < (end - start) / 2 + start; i++){
        char tmp = alpha[i];
        alpha[i] = alpha[end - i + start - 1];
        alpha[end - i + start - 1] = tmp;
    }
}
public String reverseWords(String s) {
    char[] alpha = s.toCharArray();
    int n = s.length();
    int start = 0;
    for(int i = 0; i < n; i++){
        if(alpha[i] == ' '){
            reverse(alpha, start, i);
            start = i + 1;
        }
    }
    reverse(alpha, start, n);
    return String.valueOf(alpha);
}
```
