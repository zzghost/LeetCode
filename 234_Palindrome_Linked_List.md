# Palindrome Linked List
DescriptionHintsSubmissionsDiscussSolution
Given a singly linked list, determine if it is a palindrome.

Example 1:
```
Input: 1->2
Output: false
```
Example 2:
```
Input: 1->2->2->1
Output: true
```
**Follow up:**  
Could you do it in O(n) time and O(1) space?

## Solution
Reverse the right-half part and compare with the left-half one.  
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
    public int getLength(ListNode p){
        int count = 0;
        while(p != null){
            count++;
            p = p.next;
        }
        return count;
    }
    public boolean isPalindrome(ListNode head) {
        ListNode p = head;
        int len = getLength(p);
        int count = (len % 2 == 0) ? len / 2 : len / 2 + 1;
        p = head;
        while(count != 0){
            count--;
            p = p.next;
        }
        ListNode newHead = new ListNode(0), curr = null;
        while(p != null){
            ListNode next = p.next;
            p.next = curr;
            curr = p;
            newHead.next = p;
            p = next;
        }
        p = newHead.next;
        while(p != null){
            if(p.val == head.val){
                p = p.next;
                head = head.next;
            }
            else{
                return false;
            }
        }
        return true;
    }
}
```
