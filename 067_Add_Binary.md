# Add Binary
Given two binary strings, return their sum (also a binary string).

For example,
a = `"11"`
b = `"1"`
Return `"100"`.

## Solution
**Complexity: Time O(max(m, n))**
```java
class Solution {
    public String addBinary(String a, String b) {
        int m = a.length(), n = b.length();
        int count = 0, i = m - 1, j = n - 1;
        StringBuilder sb = new StringBuilder();
        while(i >= 0 || j >= 0){
            int sum = count;
            if(j >= 0) sum += b.charAt(j--) - '0';
            if(i >= 0) sum += a.charAt(i--) - '0';
            sb.append(sum % 2);
            count = sum / 2;
        }
        if(count != 0) sb.append(count);
        return sb.reverse().toString();

    }
}
```
