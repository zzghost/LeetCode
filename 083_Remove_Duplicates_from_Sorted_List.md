# Remove Duplicates from Sorted List
## Description
Given a sorted linked list, delete all duplicates such that each element appear only once.  

For example,  
Given `1->1->2`, return `1->2`.  
Given `1->1->2->3->3`, return `1->2->3`.  
## Solution
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
    public ListNode deleteDuplicates(ListNode head) {
        if(head == null || head.next == null) return head;
        ListNode p1 = head, p2 = head.next;
        while(p2 != null){
            if(p1.val == p2.val){
                while(p2 != null && p1.val == p2.val){
                    p2 = p2.next;
                }
                p1.next = p2;
            }
            else{
                p1 = p2;
                p2 = p2.next;
            }
        }
        return head;
    }
}
```
