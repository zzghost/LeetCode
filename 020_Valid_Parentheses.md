# Valid Parentheses
## Description
Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.

## Solution
Use Stack.  
**Compelxity: Time O(n), Space O(n).**
```java
class Solution {
    public boolean isValid(String s) {
        if(s == null || s.length() == 0)
            return true;

        int n = s.length();
        if(n % 2 != 0)
            return false;
        Stack<Character> stack = new Stack<>();
        for(int i = 0; i < n; i++){
            if(s.charAt(i) == '(' || s.charAt(i) == '{' || s.charAt(i) == '[')
                stack.push(s.charAt(i));
            else if(s.charAt(i) == ')' || s.charAt(i) == '}' || s.charAt(i) == ']'){
                if(stack.isEmpty())
                    return false;
                char tp = stack.pop();
                if((tp == '(' && s.charAt(i) == ')') || (tp == '{' && s.charAt(i) == '}') || (tp == '[' && s.charAt(i) == ']'))
                    continue;
                else
                    return false;
            }
            else
                return false;
        }
        return (stack.isEmpty());
    }
}
```
