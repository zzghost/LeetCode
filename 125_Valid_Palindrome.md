# Valid Palindrome
## Description
Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.  

For example,  
```
"A man, a plan, a canal: Panama" is a palindrome.
"race a car" is not a palindrome.
```
**Note:**
Have you consider that the string might be empty? This is a good question to ask during an interview.  

For the purpose of this problem, we define empty string as valid palindrome.  
## Solution
**Complexity: Time O(n), Space O(n).**
```java
public boolean isPalindrome(String s) {
    if(s == null || s.length() == 0)
        return true;
    String t = s.toLowerCase();
    char[] alpha = t.toCharArray();
    int n = t.length();
    int left = 0, right = n - 1;
    while(left < right){
        while(left < right && !(alpha[left] >= 'a' && alpha[left] <= 'z' || alpha[left] >= '0' && alpha[left] <= '9'))
            left++;
        while(left < right && !(alpha[right] >= 'a' && alpha[right] <= 'z' || alpha[right] >= '0' && alpha[right] <= '9'))
            right--;
        if(alpha[left] == alpha[right]){
            left++;
            right--;
        }
        else{
            return false;
        }
    }
    return true;
}
```
