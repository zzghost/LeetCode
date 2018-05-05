# Merge Two Sorted Lists
## Description
Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.  
## Solution
**Complexity: O(max(m, n)).**
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
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if(l1 == null) return l2;
        if(l2 == null) return l1;
        ListNode head = l1;
        ListNode p1 = l1, p2 = l2, pre = null, post = p2;

        while(p1 != null && p2 != null){
            if(p1.val <= p2.val){
                pre = p1;
                p1 = p1.next;
                continue;
            }
            else{
                post = p2.next;
                if(pre == null){
                    pre = p2;
                    head = l2;
                }
                else
                    pre.next = p2;
                p2.next = p1;
                p2 = post;
                if(pre.next != p1)
                    pre = pre.next;
            }
        }
        if(p2 != null){
            pre.next = p2;
        }
        return head;
    }
}
```

More concise version:  
Use a `tempHead` pretending that we create a new linked list.  
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
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode tempHead = new ListNode(0);
        ListNode pre = tempHead;
        while(l1 != null && l2 != null){
            if(l1.val > l2.val){
                pre.next = l2;
                l2 = l2.next;
            }
            else{
                pre.next = l1;
                l1 = l1.next;
            }
            pre = pre.next;
        }
        if(l1 != null){
            pre.next = l1;
        }
        if(l2 != null){
            pre.next = l2;
        }
        return tempHead.next;
    }
}
```
