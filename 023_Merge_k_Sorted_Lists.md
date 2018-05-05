# Merge k Sorted Lists
Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.
## Solution
1. Use `Priority Queue`.    
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
2. Divide and Conquer  
Divide recursively and merge two lists.  
**Complexity: Time O(kNlogk), Space O(n).**  
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
    public ListNode listMerge(ListNode l1, ListNode l2){
        ListNode newHead = new ListNode(0), p = newHead;
        while(l1 != null && l2 != null){
            if(l1.val <= l2.val){
                p.next = l1;
                l1 = l1.next;
            }
            else{
                p.next = l2;
                l2 = l2.next;
            }
             p = p.next;
        }
        if(l1 != null){
          p.next = l1;
        }
        if(l2 != null){
            p.next = l2;
        }
        return newHead.next;    
    }
    public ListNode mergeKLists(ListNode[] lists) {
        if(lists == null || lists.length == 0){
            return null;
        }
        if(lists.length == 1){
            return lists[0];
        }
        if(lists.length == 2){
            return listMerge(lists[0], lists[1]);
        }

        int mid = lists.length / 2;
        ListNode[] subList1 = new ListNode[mid];
        ListNode[] subList2 = new ListNode[mid + 1];
        for(int i = 0, k = 0; i < mid && k < mid; i++, k++){
            subList1[k] = lists[i];
        }
        for(int i = mid, k = 0; i < lists.length && k <= mid; i++, k++){
            subList2[k] = lists[i];
        }
        ListNode l1 = mergeKLists(subList1);
        ListNode l2 = mergeKLists(subList2);
        return listMerge(l1, l2);
    }
}
```
