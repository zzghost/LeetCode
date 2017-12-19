# Generate Parentheses
Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:
```
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```
## Solution
BackTracking.
```java
class Solution {
  List<String> rst = new ArrayList<>();
  public void find(int left, int right, StringBuilder sb){
    if(left > right) return;//avoid ")("
      if(left == 0 && right == 0){
          rst.add(new String(sb.toString()));
          return ;
      }
      if(left > 0){
        sb.append("(");
        find(left - 1, right, sb);
        sb.deleteCharAt(sb.length() - 1);
      }
      if(right > 0){
          sb.append(")");
          find(left, right - 1, sb);
          sb.deleteCharAt(sb.length() - 1);
      }
  }
  public List<String> generateParenthesis(int n) {
      StringBuilder sb = new StringBuilder();
      find(n, n, sb);
      return rst;
  }
}
```
