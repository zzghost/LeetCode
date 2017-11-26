# Insert Interval
## Description
Given a set of non-overlapping intervals, insert a new interval into the intervals (merge if necessary).

You may assume that the intervals were initially sorted according to their start times.

Example 1:
Given intervals `[1,3],[6,9]`, insert and merge `[2,5]`in as `[1,5],[6,9]`.

Example 2:
Given `[1,2],[3,5],[6,7],[8,10],[12,16]`, insert and merge `[4,9]` in as `[1,2],[3,10],[12,16]`.

This is because the new interval `[4,9]` overlaps with `[3,5],[6,7],[8,10]`.
## Solution
Traversal.  
**Complexity: Time O(n), Space O(1).**
```java
/**
 * Definition for an interval.
 * public class Interval {
 *     int start;
 *     int end;
 *     Interval() { start = 0; end = 0; }
 *     Interval(int s, int e) { start = s; end = e; }
 * }
 */
class Solution {
    public boolean overlap(Interval x, Interval y){
        return (x.end >= y.start && x.end <= y.end ||
               x.start >= y.start && x.start <= y.end ||
               x.start <= y.start && x.end >= y.end ||
               x.start >= y.start && x.end <= y.end);
    }
    public List<Interval> insert(List<Interval> intervals, Interval newInterval) {
        List<Interval> rst = new ArrayList<>();
        if(intervals == null || intervals.size() == 0){
            rst.add(newInterval);
            return rst;
        }
        int n = intervals.size();
        Interval x = new Interval(newInterval.start, newInterval.end);
        boolean added = false;
        for(int i = 0; i < n; ){
            Interval tmp = intervals.get(i);
            if(overlap(tmp, x)){
                int start = Math.min(x.start, tmp.start), end = x.end;
                while(i < n && overlap(intervals.get(i), x)){
                    end = Math.max(end, intervals.get(i).end);
                    x = new Interval(start, end);
                    i++;
                }
                rst.add(x);
                added = true;
                for(int j = i; j < n; j++){
                    rst.add(new Interval(intervals.get(j).start, intervals.get(j).end));
                }
                break;
            }
            else{
                if(tmp.end < x.start){
                    rst.add(new Interval(tmp.start, tmp.end));
                    i++;
                }
                else{
                    rst.add(new Interval(x.start, x.end));
                    added = true;
                    for(int j = i; j < n; j++)
                        rst.add(intervals.get(j));
                    break;
                }
            }
        }
        if(!added){
            rst.add(x);
        }
        return rst;
    }
}
```
More concise version:
```java
/**
 * Definition for an interval.
 * public class Interval {
 *     int start;
 *     int end;
 *     Interval() { start = 0; end = 0; }
 *     Interval(int s, int e) { start = s; end = e; }
 * }
 */
class Solution {
    public List<Interval> insert(List<Interval> intervals, Interval newInterval) {
        List<Interval> rst = new ArrayList<>();
        int n = intervals.size(), i = 0;
        //add the previous which are lower than newInterval.
        while(i < n && intervals.get(i).end < newInterval.start){
            rst.add(new Interval(intervals.get(i).start, intervals.get(i).end));
            i++;
        }

        while(i < n && intervals.get(i).start <= newInterval.end){
            newInterval = new Interval(Math.min(intervals.get(i).start, newInterval.start), Math.max(intervals.get(i).end, newInterval.end));
            i++;
        }
        rst.add(newInterval);
        while(i < n)
            rst.add(intervals.get(i++));
        return rst;
    }
}
```
