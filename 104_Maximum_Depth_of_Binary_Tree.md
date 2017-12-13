# Maximum Depth of Binary Tree
## Description
Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.
## Solution
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
    public int depth(TreeNode t){
        if(t == null) return 0;
        if(t.left == null && t.right == null) return 1;
        return Math.max(depth(t.left), depth(t.right)) + 1;
    }
    public int maxDepth(TreeNode root) {
        return depth(root);
    }
}
```
