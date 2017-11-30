# Remove Duplicates from Sorted Linked List II
## Description
Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.

For example,  
Given `1->2->3->3->4->4->5`, return `1->2->5`.  
Given `1->1->1->2->3`, return `2->3`.
## Solution
** Complexity: Time O(n),Space O(1).**
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
    public ListNode deleteDuplicates(ListNode head) {
        if(head == null || head.next == null) return head;

        ListNode p1 = head, p2 = head.next, pre = null;
        while(p2 != null){
            if(p1.val != p2.val){
                pre = p1;
                p1 = p2;
                p2 = p2.next;
            }
            else{
                while(p2 != null && p1.val == p2.val){
                    p2 = p2.next;
                }
                if(pre == null){
                    head = p2;
                    pre = p2;
                }
                else if(head == p1 && pre == p1){
                  //[1,1,2,2,3]
                    pre = p2;
                    head = p2;
                }
                else
                    pre.next = p2;
                if(p2 != null){
                    p1 = p2;
                    p2 = p2.next;
                }
            }

        }
        return head;
    }
}
```
