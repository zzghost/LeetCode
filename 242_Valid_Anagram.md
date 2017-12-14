# Valid Anagram
Given two strings s and t, write a function to determine if t is an anagram of s.

For example,
s = "anagram", t = "nagaram", return true.
s = "rat", t = "car", return false.

**Note:**  
You may assume the string contains only lowercase alphabets.

**Follow up:**  
What if the inputs contain unicode characters? How would you adapt your solution to such case?


## Solution
1. Sort and pick  
**Complexity: Time O(nlogn), Space O(1).**
2. HashMap  
**Complexity: Time O(n), Space O(1).**
3. Use array(Optimal)
**Complexity: Time O(n), Space O(1).**
```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if(s.length() != t.length()) return false;
        int n = s.length();
        int[] count = new int[26];
        for(int i = 0; i < n; i++){
            count[s.charAt(i) - 'a']++;
            count[t.charAt(i) - 'a']--;
        }
        for(int i: count)
            if(i != 0)
                return false;
        return true;
    }
}
```
