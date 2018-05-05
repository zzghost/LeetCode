# Remove K Digits
## Description
Given a non-negative integer num represented as a string, remove k digits from the number so that the new number is the smallest possible.

**Note:**  
+ The length of num is less than 10002 and will be ≥ k.
+ The given num does not contain any leading zero.

**Example 1:**
```
Input: num = "1432219", k = 3
Output: "1219"
Explanation: Remove the three digits 4, 3, and 2 to form the new number 1219 which is the smallest.
```
**Example 2:**
```
Input: num = "10200", k = 1
Output: "200"
Explanation: Remove the leading 1 and the number is 200. Note that the output must not contain leading zeroes.
```
**Example 3:**
```
Input: num = "10", k = 2
Output: "0"
Explanation: Remove all the digits from the number and it is left with nothing which is 0.
```
## Solution
**Greedy**  
Use a `stack` to store the result string.  
It can be pointed that we delete from highest position and the largest number.  
Besides, be aware of `10200` and `k = 1`, leading zeroes should be deleted but not counted.  
**Complexity: Time O(n), Space O(n).**  
```java
class Solution {
    public String removeKdigits(String num, int k) {
        Stack<Integer> st = new Stack<>();
        int n = num.length();
        for(int i = 0; i < n; i++){
            int number = num.charAt(i) - '0';
            //when st.peek() is larger than number, keep deleting
            while(st.size() != 0 && st.peek() > number && k > 0){
                st.pop();
                k--;
            }
            //when stack is empty and number=0, do not push
            //which deletes the leading zeroes
            if(st.size() != 0 || number != 0){
                st.push(number);
            }
        }
        //in case k != 0
        while(k > 0 && !st.isEmpty()){
            st.pop();
            k--;
        }
        StringBuilder sb = new StringBuilder();
        while(!st.isEmpty()){
            sb.append(st.pop());
        }
        if(sb.length() == 0){
            return "0";
        }
        return sb.reverse().toString();
    }
}
```
