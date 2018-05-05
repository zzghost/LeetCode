# Simplify path
## Description
Given an absolute path for a file (Unix-style), simplify it.

For example,
path = "/home/", => "/home"
path = "/a/./b/../../c/", => "/c"

Corner Cases:

Did you consider the case where path = "/../"?
In this case, you should return "/".
Another corner case is the path might contain multiple slashes '/' together, such as "/home//foo/".
In this case, you should ignore redundant slashes and return "/home/foo".

## Solution
Split the string and use stack to store each word.  
```java
class Solution {
    public String simplifyPath(String path) {
        String[] paths = path.split("/");
        Stack<String> stack = new Stack<>();
        for(String str : paths){
            if(str.equals(".")){
                continue;
            }
            if(str.equals("..")){
                if(!stack.isEmpty()){
                    stack.pop();
                }
            }
            else{
                if(!str.equals("")){
                    stack.push(str);
                }
            }
        }
        StringBuilder sb = new StringBuilder();
        if(stack.isEmpty()){
            sb.append("/");
            return sb.toString();
        }
        while(!stack.isEmpty()){
            sb.insert(0, "/");
            sb.insert(1, stack.pop());
        }
        return sb.toString();
    }
}
```
