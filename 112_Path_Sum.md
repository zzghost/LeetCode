# Path Sum
## Description
Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

For example:
Given the below binary tree and `sum = 22`,
```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \      \
        7    2      1
```
return true, as there exist a root-to-leaf path `5->4->11->2` which sum is 22.
## Solution
Depth-first traversal.  
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
    public boolean find(TreeNode current, int sum){
        if(current == null)
            return false;
        if(current.left == null && current.right == null){
            return (sum == current.val);
        }
        else{
            return find(current.left, sum - current.val) || find(current.right, sum - current.val);
        }
    }
    public boolean hasPathSum(TreeNode root, int sum) {
        return find(root, sum);
    }
}
```
