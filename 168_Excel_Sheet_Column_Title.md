# Excel Sheet Column Title
Given a positive integer, return its corresponding column title as appear in an Excel sheet.

For example:
```
    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB
```
## Solution
```java
class Solution {
    public String convertToTitle(int n) {
        char[] ALPHA = new char[26];
        for(int i = 0; i < 26; i++){
            ALPHA[i] = (char)('A' + i);
        }
        StringBuilder sb = new StringBuilder();
        int seed = 0;
        while(n > 0){
            int remain = n % 26, shang = n / 26;
            if(remain == 0 && shang != 0){
                sb.append("Z");
                shang--;
            }
            else{
                if(remain != 0){
                    sb.append(ALPHA[remain - 1]);
                }
            }
            n = shang;
        }
        return sb.reverse().toString();
    }
}
```
