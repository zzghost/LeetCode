# 141. Linked List Cycle
## Description
Given a linked list, determine if it has a cycle in it.

Follow up:
Can you solve it without using extra space?
## Solution
Two pointers.  
One faster and another slower.  
**Complexity: Time O(n), Space O(1)**
```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        if(head == null || head.next == null) return false;

        ListNode p1 = head, p2 = head.next;
        while(p2 != null){
            if(p1.val == p2.val)
                return true;
            p1 = p1.next;
            if(p2.next != null)
                p2 = p2.next.next;
            else
                return false;
        }
        return false;
    }
}
```
