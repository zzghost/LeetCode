# Add Two Numbers II
## Description
You are given two non-empty linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Follow up:
What if you cannot modify the input lists? In other words, reversing the lists is not allowed.

Example:
```
Input: (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 8 -> 0 -> 7
```
## Solution
Just like Two linked list find the common node. Longer list go first ,store the value in array.  
The array stores each node's sum. And finally process the array.  
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
    public int getLength(ListNode l){
        int len = 0;
        while(l != null){
            len++;
            l = l.next;
        }
        return len;
    }
    public ListNode goFirst(ListNode p, int diff, int[] sum, int idx){
        while(p != null && diff != 0){
            sum[idx++] = p.val;
            p = p.next;
            diff--;
        }
        return p;
    }
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode p1 = l1, p2 = l2;
        int m = getLength(p1), n = getLength(p2);
        int[] sum = new int[Math.max(m, n)];
        int diff = Math.abs(m - n), i = diff;
        //longer list go first
        if(m > n)
            p1 = goFirst(p1, diff, sum, 0);
        else
            p2 = goFirst(p2, diff, sum, 0);
        //add the sum and process the carry
        while(p1 != null){
            sum[i++] = p1.val + p2.val;
            p1 = p1.next;
            p2 = p2.next;
        }
        int carry = 0;
        for(int j = sum.length - 1; j >= 0; j--){
            sum[j] += carry;
            carry = sum[j] / 10;
            sum[j] = sum[j] % 10;
        }
        //store in linked list
        ListNode head = null;
        if(carry != 0)
            head = new ListNode(carry);
        p1 = head;
        for(int j = 0; j < sum.length; j++){
            ListNode tmp = new ListNode(sum[j]);
            if(p1 != null){
                p1.next = tmp;
                p1 = p1.next;
            }
            else{
                p1 = tmp;
                head = p1;
            }
        }

        return head;
    }
}
```
