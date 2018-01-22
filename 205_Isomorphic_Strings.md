# Isomorphic Strings
Given two strings s and t, determine if they are isomorphic.

Two strings are isomorphic if the characters in s can be replaced to get t.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.

For example,
Given "egg", "add", return true.

Given "foo", "bar", return false.

Given "paper", "title", return true.

**Note:**  
You may assume both s and t have the same length.
## Solution
Use `HashMap` can be very intuitive.   
Here we can use `int[] array` which avoid the case "ab","aa".  
```java
class Solution {
    public boolean isIsomorphic(String s, String t) {
        if (s == null || t == null || s.length() != t.length()) {
            return false;
        }
        int[] sMap = new int[256], tMap = new int[256];
        int n = s.length();
        for (int i = 0; i < n; i++) {
            char sChar = s.charAt(i), tChar = t.charAt(i);
            //use the initial state for convenience.
            if (sMap[sChar] != tMap[tChar]) {
                return false;
            }
            sMap[sChar] = i + 1;   // to differential case 0, 0
            tMap[tChar] = i + 1;
        }
        return true;
    }
}
```
