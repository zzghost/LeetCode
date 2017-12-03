# Balanced Binary Tree
Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.
## Solution
**Complexity: Time O(n), Space O(n).**
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
    boolean rst = true;
    public int depth(TreeNode t){
        if(t == null) return 0;
        int left = depth(t.left);
        int right = depth(t.right);
        if(Math.abs(left - right) > 1){
            rst = false;
        }
        return (left == 0 || right == 0) ? (left + right + 1) : Math.max(left, right) + 1;
    }
    public boolean isBalanced(TreeNode root) {
        int d = depth(root);
        return rst;
    }
}
```
