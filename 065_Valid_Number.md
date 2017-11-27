# Valid Number
Validate if a given string is numeric.

Some examples:  
`"0" => true`  
`" 0.1 " => true`  
`"abc" => false`  
`"1 a" => false`  
`"2e10" => true`  
Note: It is intended for the problem statement to be ambiguous. You should gather all requirements up front before implementing one.

## Solution
A problem needs to be careful.  
Watch out the cases like:  
-e58(false), 1.2e1(true), 1e+1(true), -.(false).etc  
**Complexity: Time O(n), Space O(1).**
```java
class Solution {
    public boolean onlyHasNum(String s, int start, int end){
        int i = start;
        while(i <= end){
            if(s.charAt(i) < '0' || s.charAt(i) > '9')
                return false;
            i++;
        }
        return true;
    }
    public boolean isDecimal(String t, int start, int end){
        if(t.indexOf('.') >= 0){
            int idx = t.indexOf('.');
            if(idx != -1 && (end - start + 1) == 1)//only has "."
                return false;
            //left
            if(!onlyHasNum(t, start, idx - 1))
                return false;
            //right
            if(idx + 1 <= end && !onlyHasNum(t, idx + 1, end))
                return false;
            return true;
        }
        return false;
    }
    public boolean isNumber(String s) {
        if(s == null || s.length() == 0)
            return false;
        String t = s.trim();//eliminate the space
        int n = t.length();
        if(n == 0) return false;
        int start = 0, end = n - 1;
        if(t.charAt(start) == '+' || t.charAt(start) == '-')
            start++;
        if(t.indexOf('e') >= 0){//it's an "e" number
            int idx = t.indexOf('e');
            //left
            if(idx == start)
                return false;
            int idxOfdecimal = t.substring(start, idx).indexOf('.');
            if(idxOfdecimal >= 0){
                if(!isDecimal(t, start, idx - 1))
                    return false;
            }
            else{
                if(!onlyHasNum(t, start, idx - 1))
                    return false;
            }
            //right
            start = idx;
            if(start < n - 1 && (t.charAt(start + 1) == '+' || t.charAt(start + 1) == '-'))
                start++;
            if(start == n - 1 || !onlyHasNum(t, start + 1, end))
                return false;
        }
        else{//it's a decimal
            if(t.indexOf('.') >= 0){
                if(!isDecimal(t, start, end))
                    return false;
            }
            else{//It's an integer
                if(!onlyHasNum(t, start, end))
                    return false;
            }
        }
        return true;
    }
}
```
