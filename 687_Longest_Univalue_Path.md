# Longest Univalue Path

## Description
Given a binary tree, find the length of the longest path where each node in the path has the same value. This path may or may not pass through the root.

Note: The length of path between two nodes is represented by the number of edges between them.

Example 1:
```
Input:

              5
             / \
            4   5
           / \   \
          1   1   5
Output:

2
```
Example 2:
```
Input:

              1
             / \
            4   5
           / \   \
          4   4   5
Output:

2
```
**Note:** The given binary tree has not more than 10000 nodes. The height of the tree is not more than 1000.


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
    public int findLongest(TreeNode curr, TreeNode pre){
        if(curr == null || curr.val != pre.val){
            return 0;
        }
        return 1 + Math.max(findLongest(curr.left, curr), findLongest(curr.right, curr));
    }
    public int longestUnivaluePath(TreeNode root) {
        if(root == null){
            return 0;
        }
        int count = findLongest(root.left, root) + findLongest(root.right, root) ;
        return Math.max(count, Math.max(longestUnivaluePath(root.left), longestUnivaluePath(root.right)));
    }
}
```
