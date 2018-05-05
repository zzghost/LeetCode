# Find All Anagrams in a String
Given a string s and a non-empty string p, find all the start indices of p's anagrams in s.

Strings consists of lowercase English letters only and the length of both strings s and p will not be larger than 20,100.

The order of output does not matter.

**Example 1:**  
```
Input:
s: "cbaebabacd" p: "abc"

Output:
[0, 6]

Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
```
**Example 2:**  
```
Input:
s: "abab" p: "ab"

Output:
[0, 1, 2]

Explanation:
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
```
## Solution
1. Table
Use two table to record each character's appearance.  
In the table of s, it only records `p.length()` of characters. So when i >= p.length(), each appeared character should decremented by one.  
```java
class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        List<Integer> ans = new ArrayList<>();
        int m = s.length(), n = p.length();
        if(m < n){
            return ans;
        }
        int[] mapS = new int[26];
        int[] mapP = new int[26];
        for(Character c : p.toCharArray()){
            mapP[c - 'a']++;
        }
        for(int i = 0; i < m; i++){
            mapS[s.charAt(i) - 'a']++;
            if(i >= n){
                mapS[s.charAt(i - n) - 'a']--;
            }
            if(Arrays.equals(mapS, mapP)){
                ans.add(i - n + 1);
            }
        }
        return ans;
    }
}
```
2. Sliding Window
Window's size is p.length();
left and right pointer.
1)Expand the window's size(use right bound) and then found an element satisfies the condition, count--
2)When count == 0, we got a solution
3)Small the window's size(use left bound) and then removew the element satisfies the condition, count++
```java
class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        List<Integer> rst = new ArrayList<>();
        int m = s.length(), n = p.length();
        if(n > m){
            return rst;
        }
        int[] map = new int[256];
        for(Character c : p.toCharArray()){
            map[c]++;
        }
        int left = 0, right = 0, count = n;
        char[] ss = s.toCharArray();
        while(right < m){
          //expand the window
            if(map[ss[right++]]-- >= 1){
                count--;
            }
            //This means window's size equals to p.length()
            if(count == 0){
                rst.add(left);
            }
            //small the window
            if(right - left == n && map[ss[left++]]++ >= 0){
                count++;
            }
        }
        return rst;
    }
}
```
