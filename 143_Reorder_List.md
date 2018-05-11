# Reorder List
## Description
Given a singly linked list L: L0→L1→…→Ln-1→Ln,
reorder it to: L0→Ln→L1→Ln-1→L2→Ln-2→…

You may not modify the values in the list's nodes, only nodes itself may be changed.

Example 1:
```
Given 1->2->3->4, reorder it to 1->4->2->3.
```
Example 2:
```
Given 1->2->3->4->5, reorder it to 1->5->2->4->3.
```
## Solution
Reverse the L(n/2)- L(n) list and insert into L(1)-L(n/2-1) list.  
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
    public int countLen(ListNode head){
        ListNode p = head;
        int count = 0;
        while(p != null){
            p = p.next;
            count++;
        }
        return count;
    }
    public ListNode goFastAndReverse(ListNode head, int count){
        ListNode p = head;
        ListNode newHead = new ListNode(0), curr = null;
        ListNode pre = null;
        while(count != 0){
            pre = p;
            p = p.next;
            count--;
        }
        pre.next = null;
        while(p != null){
            ListNode next = p.next;
            p.next = curr;
            newHead.next = p;
            curr = p;
            p = next;
        }
        return newHead.next;
    }
    public void reorderList(ListNode head) {
        if(head == null){
            return ;
        }
        int len = countLen(head);
        int count = len - (len % 2 == 0 ? len / 2 - 1 : len / 2);
        ListNode newHead = goFastAndReverse(head, count);

        ListNode p = head;
        while(newHead != null){
            ListNode next = newHead.next;
            newHead.next = p.next;
            p.next = newHead;
            p = p.next.next;
            newHead = next;
        }
    }
}
```
