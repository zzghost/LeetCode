# Reverse String
## Description
Write a function that takes a string as input and returns the string reversed.  

**Example:**  
Given s = "hello", return "olleh".  

## Solution
1. Two pointers.  
**Complexity: Time O(n), Space O(n).**  
```java
public String reverseString(String s) {
    if(s == null || s.equals(""))
        return s;
    char[] c = s.toCharArray();
    int n = s.length();
    for(int i = 0; i < n / 2; i++){
        char tmp = c[n - i - 1];
        c[n - i - 1] = c[i];
        c[i] = tmp;
    }
    return String.valueOf(c);
}
```
2. Using java Libarary.  
```java
public String reverseString(String s) {
    StringBuilder sb = new StringBuilder(s);
    return sb.reverse().toString();
}
```
