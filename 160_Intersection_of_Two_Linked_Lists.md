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
1)Count each linked list's length.  
2)Move the differ nodes.  
3)Two pointers move together.  
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
    public int getLength(ListNode head){
        int length = 0;
        while(head != null){
            length++;
            head = head.next;
        }
        return length;
    }
    public ListNode moveForward(ListNode head, int count){
        while(count != 0 && head != null){
            count--;
            head = head.next;
        }
        return head;
    }
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        int aLength = getLength(headA), bLength = getLength(headB);
        if(aLength > bLength){
            headA = moveForward(headA, aLength - bLength);
        }
        else{
            headB = moveForward(headB, bLength - aLength);
        }
        while(headA != null && headB != null){
            if(headA == headB){
                return headA;
            }
            headA = headA.next;
            headB = headB.next;
        }
        return null;
    }
}
```
