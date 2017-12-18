# Remove Nth Node From End of List
## Description
Given a linked list, remove the nth node from the end of list and return its head.

For example,
```
   Given linked list: 1->2->3->4->5, and n = 2.

   After removing the second node from the end, the linked list becomes 1->2->3->5.
```
**Note:**  
Given n will always be valid.
Try to do this in one pass.
## Solution
Fast and slow pointers.  
**Complexity: Time O(n),Space O(1).**
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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode fast = head, slow = head, pre = slow;
        int count = 0;
        while(count < n && fast != null){
            fast = fast.next;
            count++;
        }
        if(fast == null)
            return head.next;
        while(fast != null){
            fast = fast.next;
            pre = slow;
            slow = slow.next;
        }
        pre.next = slow.next;
        return head;
    }
}
```
