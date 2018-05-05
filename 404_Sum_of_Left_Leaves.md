# Sum of Left Leaves
## Description
Find the sum of all left leaves in a given binary tree.

Example:
```
    3
   / \
  9  20
    /  \
   15   7

There are two left leaves in the binary tree, with values 9 and 15 respectively. Return 24.
```
## Solution
Preorder Traversal.  
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
    int sum = 0;
    public void find(TreeNode curr, TreeNode parent){
        if(curr == null){
            return ;
        }
        if(curr.left == null && curr.right == null){
            if(parent != null && parent.left == curr){
                sum += curr.val;
                return ;
            }
        }
        find(curr.left, curr);
        find(curr.right, curr);
    }
    public int sumOfLeftLeaves(TreeNode root) {
        find(root, null);
        return sum;
    }
}
```
