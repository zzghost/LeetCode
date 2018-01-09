# Group Anagrams
Given an array of strings, group anagrams together.

For example, given: ["eat", "tea", "tan", "ate", "nat", "bat"],
Return:
```
[
  ["ate", "eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```
**Note: ** All inputs will be in lower-case.  
## Solution
Use HashMap. Use alphabetic order word as key and ArrayList as value.    
**Complexity: Time O(n), Space O(n).**
```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        if(strs == null || strs.length == 0) return null;
        HashMap<String, List<String>> map = new HashMap<>();
        for(String s : strs){
            char[] tmp = s.toCharArray();
            Arrays.sort(tmp);
            String t = String.valueOf(tmp);
            if(!map.containsKey(t))
                map.put(t, new ArrayList<>());
            map.get(t).add(s);
        }
        return new ArrayList<>(map.values());
    }
}
```
