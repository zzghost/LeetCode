# Intersection of Two Linked Lists
Write a program to find the node at which the intersection of two singly linked lists begins.


For example, the following two linked lists:
```
A:          a1 → a2
                   ↘
                     c1 → c2 → c3
                   ↗            
B:     b1 → b2 → b3
begin to intersect at node c1.
```

**Notes:**  

+ If the two linked lists have no intersection at all, return null.
+ The linked lists must retain their original structure after the function returns.
+ You may assume there are no cycles anywhere in the entire linked structure.
+ Your code should preferably run in O(n) time and use only O(1) memory.

## Solution
Two pointers.  
**Complexity :Time O(n), Space O(1).**
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode p = headA, q = headB;
        int m = 0, n = 0;
        while(p != null){
            p = p.next;
            m++;
        }
        while(q != null){
            q = q.next;
            n++;
        }
        int diff = Math.abs(m - n);
        p = headA; q = headB;
        if(m > n){
            while(diff > 0){
                p = p.next;
                diff--;
            }
        }
        else{
            while(diff > 0){
                q = q.next;
                diff--;
            }
        }
        while(p != null){
            if(p.val == q.val){
                return q;
            }
            p = p.next;
            q = q.next;
        }
        return null;
    }
}
```
