# Evaluate Reverse Polish Notation
## Description
Evaluate the value of an arithmetic expression in Reverse Polish Notation.

Valid operators are ``+, -, *, /``. Each operand may be an integer or another expression.

**Note:**

Division between two integers should truncate toward zero.
The given RPN expression is always valid. That means the expression would always evaluate to a result and there won't be any divide by zero operation.
Example 1:
```
Input: ["2", "1", "+", "3", "*"]
Output: 9
Explanation: ((2 + 1) * 3) = 9
```
Example 2:
```
Input: ["4", "13", "5", "/", "+"]
Output: 6
Explanation: (4 + (13 / 5)) = 6
```
Example 3:
```
Input: ["10", "6", "9", "3", "+", "-11", "*", "/", "*", "17", "+", "5", "+"]
Output: 22
Explanation:
  ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22
```
## Solution
**Complexity: Time O(n), Space O(n).**
```java
class Solution {
    public boolean isOperator(String str){
        return (str.equals("+")) || (str.equals("-") || (str.equals("*")) || (str.equals("/")));
    }
    public int helper(int num1, int num2, String str){
        switch(str){
            case"+": return num1 + num2;
            case "-": return num2 - num1;
            case "*": return num1 * num2;
            default: return num2 / num1;
        }
    }
    public int evalRPN(String[] tokens) {
        Stack<Integer> numbers = new Stack<>();
        for(String str: tokens){
            if(isOperator(str)){
                int num1 = numbers.pop(), num2 = numbers.pop();
                int rst = helper(num1, num2, str);
                numbers.push(rst);
            }
            else{
                numbers.push(Integer.parseInt(str));
            }
        }
        return numbers.pop();
    }
}
```
