# Longest Substring Without Repeating Characters
Given a string, find the length of the longest substring without repeating characters.

Examples:

Given ``"abcabcbb"``, the answer is ``"abc"``, which the length is 3.

Given ``"bbbbb"``, the answer is ``"b"``, with the length of 1.

Given ``"pwwkew"``, the answer is ``"wke"``, with the length of 3. Note that the answer must be a substring, ``"pwke"`` is a subsequence and not a substring.
## Solution
Two Pointers + HashMap.  
Right pointer to traverse.  
Left pointer will point to the same character last found.  
HashMap stores the latest position of the character.  
```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        if(s.length() == 0) return 0;
        Map<Character, Integer> map = new HashMap<Character, Integer>();
        int count = 0;
        for(int i = 0, j = 0; i < s.length(); i++){
            if(map.containsKey(s.charAt(i)))
                j = Math.max(j, map.get(s.charAt(i)) + 1);
            map.put(s.charAt(i), i);
            count = Math.max(count, i - j + 1);
        }
        return count;
    }
}
```
