# Swap Nodes in Pairs
Given a linked list, swap every two adjacent nodes and return its head.

For example,
Given `1->2->3->4`, you should return the list as `2->1->4->3`.

Your algorithm should use only constant space. You may not modify the values in the list, only nodes itself can be changed.

## Solution
Three pointers:pre, current and post.  

**Complexity: Time O(n), Space O(1).**
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
    public ListNode swapPairs(ListNode head) {
        if(head == null || head.next == null) return head;
        ListNode pre = null, p = head, post = head.next;
        while(post != null){
            ListNode tmp = post.next;
            post.next = p;
            p.next = tmp;
            //deal the head of the linked list.  
            if(pre == null){
                head = post;
                pre = head.next;
            }
            else{
                pre.next = post;
                pre = pre.next.next;
            }
            if(tmp == null) break;
            post = tmp.next;
            p = tmp;
        }
        return head;
    }
}
```
