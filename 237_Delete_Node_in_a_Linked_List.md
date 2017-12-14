# Delete Node in a Linked List
## Description

Write a function to delete a node (except the tail) in a singly linked list, given only access to that node.

Supposed the linked list is `1 -> 2 -> 3 -> 4` and you are given the third node with value 3, the linked list should become` 1 -> 2 -> 4` after calling your function.

## Solution
**Complexity: O(n), Space O(1)**
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
    public void deleteNode(ListNode node) {
        ListNode p = node, pre = null;
        while(p.next != null){
            p.val = p.next.val;
            pre = p;
            p = p.next;
        }
        pre.next = null;
    }
}
```
