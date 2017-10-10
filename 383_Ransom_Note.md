# Ransom Note
## Description
Given an arbitrary ransom note string and another string containing letters from all the magazines, write a function that will return true if the ransom note can be constructed from the magazines ; otherwise, it will return false.  

Each letter in the magazine string can only be used once in your ransom note.  

**Note:**
You may assume that both strings contain only lowercase letters.
```
canConstruct("a", "b") -> false
canConstruct("aa", "ab") -> false
canConstruct("aa", "aab") -> true
```


## Solution
1. Use record array.
**Complexity: Time O(n), Space O(n).**
```java
public boolean canConstruct(String ransomNote, String magazine) {
    char[] notes = ransomNote.toCharArray();
    char[] mag = magazine.toCharArray();

    int[] table = new int[26];
    for(Character c : mag)
        table[c - 'a']++;

    for(Character c : notes)
        if(--table[c - 'a'] < 0)
            return false;
    return true;
}
```
2. Use HashMap.
**Complexity: Time O(n), Space O(n).**
```java
public boolean canConstruct(String ransomNote, String magazine) {
    Map<Character, Integer> map = new HashMap<>();
    char[] notes = ransomNote.toCharArray();
    char[] mag = magazine.toCharArray();

    for(Character c : mag)
        map.put(c, map.getOrDefault(c, 0) + 1);

    for(Character c : notes){
        if(map.containsKey(c)){
            if(map.get(c) > 0)
                map.put(c, map.get(c) - 1);
            else
                return false;
        }
        else
            return false;
    }
    return true;
}
```
3. Sorting.
**Complexity: Time O(nlogn), Space O(1).**
```java
public boolean canConstruct(String ransomNote, String magazine) {
    char[] notes = ransomNote.toCharArray();
    char[] mag = magazine.toCharArray();

    Arrays.sort(notes);
    Arrays.sort(mag);
    int i = 0, j = 0, n = notes.length, m = mag.length;
    while(i < n && j < m){
        while(i < n && j < m && notes[i] == mag[j]){
            i++;j++;
        }
        if(i == n)
            return true;
        while(j < m && notes[i] != mag[j])
            j++;
        if(j == m && i != n)
            return false;
    }
    if(i == n)
        return true;
    else
        return false;
}
```
