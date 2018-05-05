# Partition List
Given a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.

You should preserve the original relative order of the nodes in each of the two partitions.

For example,
Given `1->4->3->2->5->2` and x = 3,
return `1->2->2->4->3->5`.
## Solution
Use two temp ListNode head.One stores smaller than x nodes, another stores larger than and equals with x.  
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
    public ListNode partition(ListNode head, int x) {
        ListNode smallerHead = new ListNode(0), largeHead = new ListNode(0);
        ListNode lessP = smallerHead, largeP = largeHead;
        while(head != null){
            if(head.val < x){
                lessP.next = head;
                lessP = head;
            }
            else{
                largeP.next = head;
                largeP = head;
            }
            head = head.next;
        }
        lessP.next = largeHead.next;
        largeP.next = null;
        return smallerHead.next;

    }
}
```
