# Reverse Linked List II
Reverse a linked list **from position m to n**. Do it in-place and in one-pass.

For example:
Given 1->2->3->4->5->NULL, m = 2 and n = 4,

return 1->4->3->2->5->NULL.

**Note:**  
Given m, n satisfy the following condition:
1 ≤ m ≤ n ≤ length of list.
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
    public ListNode reverseBetween(ListNode head, int m, int n) {
        ListNode p = head, q = head, k = head, pre = null;
        int count1 = 1, count2 = 1;
        while(count2 < n){
            if(count1 < m){
                pre = p;
                p = p.next;
                count1++;
            }
            q = q.next;
            count2++;
        }
        if(pre != null)
            pre.next = q;
        else
        //m = 1
            head = q;
        while(p != q){
            ListNode tmp = p.next;
            p.next = q.next;
            q.next = p;
            p = tmp;
        }
        return head;
    }
}
```
