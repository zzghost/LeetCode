# Merge Intervals
## Description
Given a collection of intervals, merge all overlapping intervals.  

For example,  
```
Given [1,3],[2,6],[8,10],[15,18],
return [1,6],[8,10],[15,18].
```
## Solution
1. Lamda expression.  
**Complexity: Time O(nlogn), Space O(n).**
```java
public List<Interval> merge(List<Interval> intervals) {
    if(intervals == null || intervals.size() <= 1)
        return intervals;

    List<Interval> list = new ArrayList<Interval>();
    //java8 lambda expression
    intervals.sort((i1, i2) -> Integer.compare(i1.start, i2.start));

    int start = intervals.get(0).start;
    int end = intervals.get(0).end;
    for(Interval item : intervals){
        if(item.start <= end)
            end = Math.max(end, item.end);
        else{
            list.add(new Interval(start, end));
            start = item.start;
            end = item.end;
        }
    }
    list.add(new Interval(start, end));
    return list;
}
```
2. Store starts and ends.
**Complexity: Time O(nlogn), Space O(n).**
```java
public List<Interval> merge(List<Interval> intervals) {
    if(intervals == null || intervals.size() <= 1)
        return intervals;

    List<Interval> list = new ArrayList<Interval>();
    int n = intervals.size();
    int[] starts = new int[n];
    int[] ends = new int[n];
    for(int i = 0; i < n; i++){
        starts[i] = intervals.get(i).start;
        ends[i] = intervals.get(i).end;
    }
    Arrays.sort(starts); Arrays.sort(ends);
    for(int i = 0, j = 0; i < n; i++){
        if(i == n - 1 || starts[i + 1] > ends[i]){
            list.add(new Interval(starts[j], ends[i]));
            j =  i + 1;
        }
    }
    return list;
}
```
