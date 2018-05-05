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
        ListNode slow = head, fast = head;
        ListNode meet = null;
        while(fast != null){
            slow = slow.next;
            fast = fast.next;
            if(fast == null){
                return null;
            }
            fast = fast.next;
            if(slow == fast){
                meet = fast;
                break;
            }
        }
        if(meet == null){
            return null;
        }
        while(head != null && meet != null){
          //when head meets `meet`, it's the entrance node
            if(head == meet){
                return head;
            }
            head = head.next;
            meet = meet.next;
        }
        return null;
    }
}
```
