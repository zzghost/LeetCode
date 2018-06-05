# Restore IP Addresses
## Description
Given a string containing only digits, restore it by returning all possible valid IP address combinations.

**Example:**  
```
Input: "25525511135"
Output: ["255.255.11.135", "255.255.111.35"]
```
## Solution
```java
class Solution {
    List<String> adr = new ArrayList<>();
    public boolean isValid(String str){
        boolean allZero = true;
        for(int i = 0; i < str.length(); i++){
            if(str.charAt(i) != '0'){
                allZero = false;
                break;
            }
        }
        if(str.length() > 1 && ((str.charAt(0) == '0' && allZero == false) || allZero)){
            return false;
        }
        int num = Integer.parseInt(str);
        return (num >= 0 && num < 256);
    }
    public void helper(String s, int idx, int count, List<String> subStr){
        if(count == 4){
            if(idx == s.length()){
                String rst = String.join(".", subStr);
                adr.add(rst);
            }
            return ;
        }
        for(int i = 0; i < 3; i++){
            if(idx + i >= s.length()){
                break;
            }
            String sub = s.substring(idx, idx + i + 1);
            if(isValid(sub)){
                subStr.add(sub);
                helper(s, idx + i + 1, count + 1, subStr);
                subStr.remove(subStr.size() - 1);
            }
        }
    }
    public List<String> restoreIpAddresses(String s) {
        int n = s.length();
        helper(s, 0, 0, new ArrayList<String>());
        return adr;
    }
}
```
