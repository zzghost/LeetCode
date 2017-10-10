# Reverse Vowels of a String
## Description
Write a function that takes a string as input and reverse only the vowels of a string.

Example 1:
Given s = "hello", return "holle".

Example 2:
Given s = "leetcode", return "leotcede".

**Note:**
The vowels does not include the letter "y".  
## Solution
Two pointers.
**Complexity: Time O(n), Space O(1).**
```java
public String reverseVowels(String s) {
    Set<Character> set = new HashSet<>();
    set.add('a');set.add('e');set.add('i');set.add('o');set.add('u');
    set.add('A');set.add('E');set.add('I');set.add('O');set.add('U');
    char[] str = s.toCharArray();
    int n = s.length();
    int i = 0, j = n - 1;
    while(i < j){
        while(i < j && !set.contains(str[i])) i++;
        while(i < j && !set.contains(str[j])) j--;
        if(i < j){
            char tmp = str[i];
            str[i] = str[j];
            str[j] = tmp;
            i++;j--;
        }
    }
    return String.valueOf(str);
}
```
