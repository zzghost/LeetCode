# Populating Next Right Pointers in Each Node II
Follow up for problem "[Populating Next Right Pointers in Each Node](https://github.com/zzghost/leetcode/blob/master/116_Populating_Next_Right_Pointers_in_Each_Node.md)".

What if the given tree could be any binary tree? Would your previous solution still work?

Note:

You may only use constant extra space.
For example,
Given the following binary tree,
```
         1
       /  \
      2    3
     / \    \
    4   5    7
```
After calling your function, the tree should look like:
```
         1 -> NULL
       /  \
      2 -> 3 -> NULL
     / \    \
    4-> 5 -> 7 -> NULL
```
## Solution
Two pointers.  
Just like level order traversal.  
**Complexity: Time O(n), Space O(1).**
```java
/**
 * Definition for binary tree with next pointer.
 * public class TreeLinkNode {
 *     int val;
 *     TreeLinkNode left, right, next;
 *     TreeLinkNode(int x) { val = x; }
 * }
 */
public class Solution {
    public TreeLinkNode find(TreeLinkNode tmp){
        while(tmp != null){
            if(tmp.left != null || tmp.right != null)
                break;
            tmp = tmp.next;
        }
        return tmp;
    }
    public void connect(TreeLinkNode root) {
        if(root == null || root.left == null && root.right == null)
            return ;
        TreeLinkNode pre = null, curr = root;
        while(curr != null){
            pre = curr;
            while(curr != null){
                if(curr.left != null){
                    if(curr.right != null){
                        curr.left.next = curr.right;
                    }
                    else{
                        TreeLinkNode tmp = find(curr.next);
                        if(tmp != null)
                            curr.left.next = (tmp.left == null) ? tmp.right : tmp.left;
                        else
                            curr.left.next = null;
                    }
                }
                if(curr.right != null){
                    TreeLinkNode tmp = find(curr.next);
                    if(tmp != null)
                            curr.right.next = (tmp.left == null) ? tmp.right : tmp.left;
                        else
                            curr.right.next = null;
                }
                curr = curr.next;
            }
            while(pre != null){
                if(pre.left != null){
                    curr = pre.left;
                    break;
                }
                else if(pre.right != null){
                    curr = pre.right;
                    break;
                }
                else
                    pre = pre.next;
            }
            if(pre == null)
                curr = null;
        }
    }
}
```
