# Reverse Linked List
Reverse a singly linked list.

**Hint:**  
A linked list can be reversed either iteratively or recursively. Could you implement both?
## Solution
**Complexity: Time O(n), Space O(1).**
1. Iterative
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
    public ListNode reverseList(ListNode head) {
        ListNode pre = null, p = head;
        while(p != null){
            ListNode tmp = p.next;
            p.next = pre;
            pre = p;
            p = tmp;
        }
        return pre;
    }
}
```
2. Recursive
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
    public ListNode reverse(ListNode head, ListNode newHead){
        if(head == null) return newHead;
        ListNode next = head.next;
        head.next = newHead;
        return reverse(next, head);
    }
    public ListNode reverseList(ListNode head) {
        return reverse(head, null);
    }
}
```
