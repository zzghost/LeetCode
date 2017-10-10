# Judge Route Circle
## Description
Initially, there is a Robot at position (0, 0). Given a sequence of its moves, judge if this robot makes a circle, which means it moves back to the original place.

The move sequence is represented by a string. And each move is represent by a character. The valid robot moves are R (Right), L (Left), U (Up) and D (down). The output should be true or false representing whether the robot makes a circle.

**Example 1:**
```
Input: "UD"
Output: true
```
**Example 2:**
```
Input: "LL"
Output: false
```
## Solution
**Complexity: Time O(n), Space O(n)**
```java
public boolean judgeCircle(String moves) {
    char[] move = moves.toCharArray();
    int n = moves.length();

    int sum = 0;
    for(int i = 0; i < n; i++){
        switch(move[i]){
            case 'L' : sum--;break;
            case 'R' : sum++;break;
            case 'U' : sum += 2; break;
            case 'D' : sum -= 2; break;
        }
    }
    return (sum == 0);
}
```
