# Partition List
Given a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.

You should preserve the original relative order of the nodes in each of the two partitions.

For example,
Given `1->4->3->2->5->2` and x = 3,
return `1->2->2->4->3->5`.
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
    public ListNode partition(ListNode head, int x) {
        ListNode p = null, q = head, pre = null;
        //skip the smaller one
        while(q != null && q.val < x){
            p = q;
            pre = q;
            q = q.next;
        }
        while(q != null){
            if(q.val >= x){
                pre = q;
                q = q.next;
            }
            else{
                ListNode tmp = q.next;
                if(p == null){
                    q.next = head;
                    head = q;
                }
                else{
                    q.next = p.next;
                    p.next = q;
                }
                p = q;
                pre.next = tmp;
                q = tmp;
            }
        }


        return head;
    }
}
```
