# Remove Linked List Elements
Remove all elements from a linked list of integers that have value val.

Example
Given: 1 --> 2 --> 6 --> 3 --> 4 --> 5 --> 6, val = 6
Return: 1 --> 2 --> 3 --> 4 --> 5
## Solution
Traversal.  
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
    public ListNode removeElements(ListNode head, int val) {
        ListNode pre = null, p = head;
        while(p != null){
            if(p.val == val){
                if(pre == null){
                    p = p.next;
                    head = pre;
                }
                else{
                    ListNode tmp = p.next;
                    pre.next = tmp;
                    p = tmp;
                }
            }
            else{
                pre = p;
                p = p.next;
            }
            if(head == null){
                head = pre;
            }
        }
        return head;
    }
}
```
