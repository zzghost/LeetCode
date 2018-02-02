# Merge k Sorted Lists
Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.
## Solution
Use `Priority Queue`.  
**Complexity: Time O(kn), Space O(kn)**
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        if(lists == null || lists.length == 0) return null;
        PriorityQueue<ListNode> pq = new PriorityQueue<>(lists.length, new Comparator<ListNode>(){
            public int compare(ListNode l1, ListNode l2){
                return (l1.val - l2.val);
            }
        });
        for(ListNode node : lists)
        //this case : [[]]
            if(node != null)
                pq.add(node);
        ListNode head = pq.poll(), p = head;
        if(p != null && p.next != null) pq.add(p.next);
        if(head != null)
            head.next = null;
        while(pq.size() != 0){
            p.next = pq.poll();
            p = p.next;
            if(p.next != null)
                pq.add(p.next);
            p.next = null;
        }
        return head;
    }
}
```
