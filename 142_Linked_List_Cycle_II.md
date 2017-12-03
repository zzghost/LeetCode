# Linked List Cycle II
Given a linked list, return the node where the cycle begins. If there is no cycle, return null.

**Note:** Do not modify the linked list.

**Follow up:**  
Can you solve it without using extra space?
## Solution
Two pointers: fast and slow.  
1. judge if has circle.fast goes 2 steps and slow goes 1.  
2. count nodes in circle, *count*  
3. fast go *count* steps, and then go together.  
**Complexity: Time O(n), Space O(1).**
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
    public ListNode detectCycle(ListNode head) {
        if(head == null || head.next == null) return null;
        ListNode p1 = head, p2 = head.next;
        while(p2 != null){
            if(p1 == p2){
                break;
            }
            p1 = p1.next;
            p2 = (p2.next == null) ? p2.next : p2.next.next;
        }

        if(p2 != null){
            int count = 1;
            p1 = p1.next;
            while(p1 != p2){
                p1 = p1.next;
                count++;
            }
            p1 = head; p2 = head;
            for(int i = 0; i < count; i++)
                p2 = p2.next;
            while(p1 != p2){
                p1 = p1.next;
                p2 = p2.next;
            }
            return p2;
        }
        else
            return null;
    }
}
```
