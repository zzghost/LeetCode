# Flatten Binary Tree to Linked List
Given a binary tree, flatten it to a linked list in-place.

For example,
Given
```
         1
        / \
       2   5
      / \   \
     3   4   6
```
The flattened tree should look like:
```
   1
    \
     2
      \
       3
        \
         4
          \
           5
            \
             6
```

Hints:
If you notice carefully in the flattened tree, each node's right child points to the next node of a pre-order traversal.
## Solution
Use pre-order's non-recursive solution
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
    public void flatten(TreeNode root) {
        if(root == null || root.left == null && root.right == null)
            return ;
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        TreeNode p = null;
        while(!stack.isEmpty()){
            TreeNode tp = stack.pop();
            if(p == null) p = tp;
            else {p.left = null; p.right = tp; p = p.right;}
            if(tp.right != null) stack.push(tp.right);
            if(tp.left != null) stack.push(tp.left);
        }
        return ;
    }
}
```
