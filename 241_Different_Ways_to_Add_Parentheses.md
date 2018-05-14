# Different Ways to Add Parentheses
## Description
Given a string of numbers and operators, return all possible results from computing all the different possible ways to group numbers and operators. The valid operators are ``+``, ``-`` and ``*``.

Example 1:
```
Input: "2-1-1"
Output: [0, 2]
Explanation:
((2-1)-1) = 0
(2-(1-1)) = 2
```
Example 2:
```
Input: "2*3-4*5"
Output: [-34, -14, -10, -10, 10]
Explanation:
(2*(3-(4*5))) = -34
((2*3)-(4*5)) = -14
((2*(3-4))*5) = -10
(2*((3-4)*5)) = -10
(((2*3)-4)*5) = 10
```
## Solution
Divide and Conquer.  
```java
class Solution {
    public List<Integer> diffWaysToCompute(String input) {
        List<Integer> rst = new ArrayList<>();
        for(int i = 0; i < input.length(); i++){
            char c = input.charAt(i);
            if(c == '+' || c == '-' || c == '*'){
                String s1 = input.substring(0, i);
                String s2 = input.substring(i + 1);
                List<Integer> part1 = diffWaysToCompute(s1);
                List<Integer> part2 = diffWaysToCompute(s2);
                for(Integer p1 : part1){
                    for(Integer p2 : part2){
                        int z = 0;
                        switch(c){
                            case '+': z = p1 + p2;break;
                            case '-': z = p1 - p2;break;
                            case '*': z = p1 * p2;break;
                        }
                        rst.add(z);
                    }
                }
            }
        }
        if(rst.size() == 0){
            rst.add(Integer.valueOf(input));
        }
        return rst;
    }
}
```
