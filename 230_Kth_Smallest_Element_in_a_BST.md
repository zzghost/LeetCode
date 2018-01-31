# Kth Smallest Element in a BST
Given a binary search tree, write a function kthSmallest to find the kth smallest element in it.

**Note:**  
You may assume k is always valid, 1 ≤ k ≤ BST's total elements.

**Follow up:**  
What if the BST is modified (insert/delete operations) often and you need to find the kth smallest frequently? How would you optimize the kthSmallest routine?


## Solution
InOrder.  
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public int rst = 0, count = 0;
    public void inorder(TreeNode p, int k){
        if(p == null) return ;
        inorder(p.left, k);
        count++;
        if(k == count){
            rst = p.val;
            return ;
        }
        inorder(p.right, k);
    }
    public int kthSmallest(TreeNode root, int k) {
        inorder(root, k);
        return rst;
    }
}
```
