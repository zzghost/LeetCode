# Repeated DNA Sequences
DescriptionHintsSubmissionsDiscussSolution
All DNA is composed of a series of nucleotides abbreviated as A, C, G, and T, for example: "ACGAATTCCG". When studying DNA, it is sometimes useful to identify repeated sequences within the DNA.

Write a function to find all the 10-letter-long sequences (substrings) that occur more than once in a DNA molecule.

Example:
```
Input: s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT"

Output: ["AAAAACCCCC", "CCCCCAAAAA"]
```
## Solution
1. Use HashMap  
**Complexity: O(n^2).**
```java
class Solution {
    public List<String> findRepeatedDnaSequences(String s) {
        HashMap<String, Integer> map = new HashMap<>();
        int n = s.length();
        List<String> rst = new ArrayList<>();
        for(int i = 0, j = 9; j < n; i++, j++){
            String tmp = s.substring(i, j + 1);
            if(map.containsKey(tmp)){
                if(map.get(tmp) == 1){
                    rst.add(tmp);
                    map.put(tmp, map.get(tmp) + 1);
                }
            }
            else{
                map.put(tmp, 1);
            }
        }
        return rst;
    }
}
```
2.Bit Manipulation  
A:0100,0001  
C:0100,0011  
G:0100,0111  
T:0101,0100  
Thus, we use the last 3 bits to differ the 4 characters.  
Each time we get the 3(multiply)10 = 30 bits to check if its in the map.  
And then we retrieve the last 27(use mask) bits and left shift 3 bits and add into another 3 bits.   
**Complexity: O(n^2).**
```java
class Solution {
    public List<String> findRepeatedDnaSequences(String s){
        List<String> rst = new ArrayList<>();
        if(s == null || s.length() < 10){
            return rst;
        }
        HashMap<Long, Integer> map = new HashMap<>();
        int i = 0, n = s.length();
        long mask = 0x7ffffff, curr = 0;
        while(i < 9){
            //retrieve first 9 characters, each is represented by its last 3 bits.
            curr = (curr << 3) | (s.charAt(i++) & 7);
        }
        while(i < n){
            curr = (curr & mask) << 3 | (s.charAt(i++) & 7);
            if(map.containsKey(curr)){
                if(map.get(curr) == 1){
                    String tmp = s.substring(i - 10, i);
                    rst.add(tmp);
                    map.put(curr, map.get(curr) + 1);
                }
            }
            else{
                map.put(curr, 1);
            }
        }
        return rst;
    }
}
```
