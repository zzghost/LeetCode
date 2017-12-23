# Rotate List
Given a list, rotate the list to the right by k places, where k is non-negative.


Example:
```
Given 1->2->3->4->5->NULL and k = 2,

return 4->5->1->2->3->NULL.
```

## Solution
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
    public ListNode rotateRight(ListNode head, int k) {
        if(head == null || head.next == null || k == 0) return head;
        ListNode p = head, pre = null, newHead;
        int count = 0;
        while(p != null){
            p = p.next;
            count++;
        }
        if(k >= count){
            if(k % count == 0)
                return head;
            else
                k = k % count;
        }

        int diff = count - k;
        p = head;
        while(diff != 0){
            diff--;
            pre = p;
            p = p.next;
        }
        pre.next = null;
        newHead = p;
        while(p.next != null)
            p = p.next;
        p.next = head;
        return newHead;
    }
}

```
