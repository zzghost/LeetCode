# Minimum Number of Arrows to Burst Balloons
## Description
There are a number of spherical balloons spread in two-dimensional space. For each balloon, provided input is the start and end coordinates of the horizontal diameter. Since it's horizontal, y-coordinates don't matter and hence the x-coordinates of start and end of the diameter suffice. Start is always smaller than end. There will be at most 104 balloons.

An arrow can be shot up exactly vertically from different points along the x-axis. A balloon with xstart and xend bursts by an arrow shot at x if xstart ≤ x ≤ xend. There is no limit to the number of arrows that can be shot. An arrow once shot keeps travelling up infinitely. The problem is to find the minimum number of arrows that must be shot to burst all balloons.

**Example:**  
```
Input:
[[10,16], [2,8], [1,6], [7,12]]

Output:
2

Explanation:
One way is to shoot one arrow for example at x = 6 (bursting the balloons [2,8] and [1,6]) and another arrow at x = 11 (bursting the other two balloons).
```
## Solution
**Greedy: When shoot one point, we shoot as more as possible.**  
1) Sort the array according to the left point.  
2) Maintain a current shoot interval. If the next point overlaps the current shoot interval, then we should update the interval.Else, we update the current shoot interval and add one shooter.  
**Complexity: Time O(n), Space O(n^2).**  
The space complexity can be optimized.  
```java
class Solution {
    public int findMinArrowShots(int[][] points) {
        if(points == null || points.length == 0){
            return 0;
        }
        List<int[]> pointsList = Arrays.asList(points);
        Collections.sort(pointsList, new Comparator<int[]>(){
          @Override
          public int compare(int[] o1, int[] o2) {
            // TODO Auto-generated method stub
            return (int)(o1[0] - o2[0]);
          }
        });
        int shooter = 1;
        int shootStart = points[0][0], shootEnd = points[0][1];
        for(int i = 1; i < points.length; i++){
            //overlapping
            if(points[i][0] >= shootStart && points[i][0] <= shootEnd){
                shootStart = points[i][0];
                //full-overlapping
                if(points[i][1] < shootEnd){
                    shootEnd = points[i][1];
                }
            }
            else{
                //no overlapping, need another shooter and update the current shoot interval
                shooter++;
                shootStart = points[i][0];
                shootEnd = points[i][1];
            }
        }
        return shooter;
    }
}

```
