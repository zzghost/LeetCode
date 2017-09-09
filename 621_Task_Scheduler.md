# Task Scheduler
## Description
Given a char array representing tasks CPU need to do. It contains capital letters A to Z where different letters represent different tasks.Tasks could be done without original order. Each task could be done in one interval. For each interval, CPU could finish one task or just be idle.

However, there is a non-negative cooling interval n that means between two same tasks, there must be at least n intervals that CPU are doing different tasks or just be idle.

You need to return the least number of intervals the CPU will take to finish all the given tasks.

## Example
```
Input: tasks = ['A','A','A','B','B','B'], n = 2
Output: 8
Explanation: A -> B -> idle -> A -> B -> idle -> A -> B.
```
**Note:**  
1. The number of tasks is in the range [1, 10000].  
2. The integer n is in the range [0, 100].  

## Solution
1. Use Priority Queue For Permutation.(Greedy)  
Fetch the most frequent task once a time, arrange it continuously(Poll the priority queue).  
The total progress is just like permutation.  
**Complexity: O(n^2), Space O(n)**  
```java
public int leastInterval(char[] tasks, int n) {
    if(tasks == null || tasks.length == 0)
        return 0;

    int len = tasks.length;
    HashMap<Character, Integer> map = new HashMap<>();
    for(int i = 0; i < len; i++){
        map.put(tasks[i], map.getOrDefault(tasks[i], 0) + 1);
    }
    PriorityQueue<Map.Entry<Character, Integer>> pq = new PriorityQueue<>((a, b) -> (a.getValue() != b.getValue()) ? (b.getValue() - a.getValue()) : (a.getKey() - b.getKey()));

    pq.addAll(map.entrySet());

    int count = 0;
    while(!pq.isEmpty()){
        int k = n + 1;//at least n intervals.
        List<Map.Entry<Character, Integer>> list = new ArrayList<>();
        while(k != 0 && !pq.isEmpty()){
            Map.Entry<Character, Integer> top = pq.poll();
            top.setValue(top.getValue() - 1);
            list.add(top);
            k--;
            count++;
        }

        for(Map.Entry<Character, Integer> entry : list)
            if(entry.getValue() > 0) pq.add(entry);//still have tasks, add back.

        if(pq.isEmpty())
            break;

        count += k;//Add k intervals.
    }
    return count;
}
```
2. No Permutation and Just Count.  
Sort and fetch the most frequent task `T`, count how many tasks (set it as `w`) have similar number with tasks `T`.  
Task `T` will take `(alpha[25] - 1) * (n + 1)` slots. Other `w` tasks will take `w` slots.  
**Complexity: Time O(n), Space O(26). Since `alpha` has fixed length, `sort()` takes O(26 * log(26)).**  
```java
public int leastInterval(char[] tasks, int n) {
    if(tasks == null || tasks.length == 0)
        return 0;

    int[] alpha = new int[26];
    for(int i = 0; i < tasks.length; i++)
        alpha[tasks[i] - 'A']++;

    Arrays.sort(alpha);

    int i = 25;
    while(i >= 0 && alpha[25] == alpha[i])
        i--;
    //In case there are no duplicate tasks.
    return Math.max(tasks.length, (alpha[25] - 1) * (n + 1) + 25 - i);
}
```
