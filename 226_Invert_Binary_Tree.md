# Invert Binary Tree
Invert a binary tree.
```
     4
   /   \
  2     7
 / \   / \
1   3 6   9
```
to
```
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```
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
    public void invert(TreeNode p){
        if(p == null)
            return ;
        TreeNode tmp = p.left;
        p.left = p.right;
        p.right = tmp;
        invert(p.left);
        invert(p.right);
    }
    public TreeNode invertTree(TreeNode root) {
        invert(root);
        return root;
    }
}
```
