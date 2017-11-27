# Add Two Numbers
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8

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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode p1 = l1, p2 = l2, pre1 = null, pre2 = null;
        int count = 0;
        while(p1 != null && p2 != null){
            int num = p1.val + p2.val + count;
            if(num >= 10){
                num -= 10;
                count = 1;
            }
            else{
                count = 0;
            }
            p2.val = num;

            pre1 = p1;
            p1 = p1.next;
            pre2 = p2;
            p2 = p2.next;
        }
        if(p1 == null && p2 == null && count == 1){
            ListNode tmp = new ListNode(1);
            pre2.next = tmp;
        }
        if(p2 != null && count == 1){
            ListNode pre = p2;
                while(p2 != null && p2.val == 9){
                    p2.val = 0;
                    pre = p2;
                    p2 = p2.next;
                }
                if(p2 == null){
                    ListNode tmp = new ListNode(1);
                    pre.next = tmp;
                }
                else{
                    p2.val++;
                }
        }
        if(p1 != null){
            if(count == 1){
                if(p1.val != 9){
                    p1.val++;
                    pre2.next = p1;
                }
                else{
                    pre2.next = p1;
                    ListNode pre = p1;
                    while(p1 != null && p1.val == 9){
                        p1.val = 0;
                        pre = p1;
                        p1 = p1.next;
                    }
                    if(p1 == null){
                        ListNode tmp = new ListNode(1);
                        pre.next = tmp;
                    }
                    else{
                        p1.val++;
                    }
                }
            }
            else{
                pre2.next = p1;
            }
        }
        return l2;
    }
}
```
