# Gas Station
There are N gas stations along a circular route, where the amount of gas at station i is `gas[i]`.

You have a car with an unlimited gas tank and it costs `cost[i]` of gas to travel from station i to its next station (i+1). You begin the journey with an empty tank at one of the gas stations.

Return the starting gas station's index if you can travel around the circuit once, otherwise return -1.

Note:
The solution is guaranteed to be unique.
## Solution
Greedy.  
`sum` records the total gas.`tank` records the gas in the tank.  
Each time when `tank < 0`, we hope that the next station will meet the condition.So `tank = 0` and `idx = i + 1`.
```java
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int n = gas.length;
        int tank = 0, idx = 0, sum = 0;
        for(int i = 0; i < n; i++){
            tank += (gas[i] - cost[i]);
            if(tank < 0){
                idx = i + 1;
                sum += tank;
                tank = 0;
            }
        }
        return (tank + sum) < 0 ? -1 : idx;
    }
}
```
