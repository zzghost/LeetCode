# Reverse Nodes in k-Group
## Description
Given a linked list, reverse the nodes of a linked list k at a time and return its modified list.

k is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of k then left-out nodes in the end should remain as it is.

Example:

Given this linked list: `1->2->3->4->5`

For k = 2, you should return: `2->1->4->3->5`

For k = 3, you should return: `3->2->1->4->5`

Note:

+ Only constant extra memory is allowed.
+ You may not alter the values in the list's nodes, only nodes itself may be changed.

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
    public ListNode reverseKGroup(ListNode head, int k) {
        if(k <= 1 || head == null || head.next == null){
            return head;
        }
        ListNode newHead = new ListNode(0), newTr = newHead;
        ListNode tr = head;
        while(tr != null){
            int count = k - 1;
            ListNode start = tr, end = tr;
            //check if >k
            while(count != 0 && start != null){
                start = start.next;
                count--;
            }
            if(count == 0 && start != null){
                //>=k,head insertion
                tr = start.next;
                ListNode tmp = start.next, curr = end;
                count = k - 1;
                while(count != 0){
                    ListNode next = curr.next;
                    curr.next = tmp;
                    tmp = curr;
                    start.next = tmp;
                    count--;
                    curr = next;
                }
                newTr.next = start;
                newTr = end;
            }
            else{
                //<k
                newTr.next = end;
                break;
            }
        }
        return newHead.next;
    }
}
```
