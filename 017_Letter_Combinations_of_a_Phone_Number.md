# Letter Combinations of a Phone Number
Given a digit string, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below.
```
Input:Digit string "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```
**Note:**  
Although the above answer is in lexicographical order, your answer could be in any order you want.
## Solution
BackTracking.
```java
class Solution {
    List<String> rst = new ArrayList<>();
    HashMap<Integer, String> button = new HashMap<>();
    public void find(String digits, int idx, StringBuilder sb){
        if(idx == digits.length()){
            rst.add(new String(sb.toString()));
            return ;
        }
        int num = digits.charAt(idx) - '0', n = button.get(num).length();
        for(int i = 0; i < n; i++){
            sb.append(button.get(num).charAt(i));
            find(digits, idx + 1, sb);
            sb.deleteCharAt(sb.length() - 1);
        }
    }
    public List<String> letterCombinations(String digits) {
        if(digits == null || digits.length() == 0) return rst;
        button.put(1, ""); button.put(2, "abc"); button.put(3, "def");
        button.put(4, "ghi"); button.put(5, "jkl"); button.put(6, "mno");
        button.put(7, "pqrs"); button.put(8, "tuv"); button.put(9, "wxyz");

        find(digits, 0, new StringBuilder());

        return rst;
    }
}
```
