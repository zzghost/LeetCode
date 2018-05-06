# Convert BST to Greater Tree
DescriptionHintsSubmissionsDiscussSolution
Given a Binary Search Tree (BST), convert it to a Greater Tree such that every key of the original BST is changed to the original key plus sum of all keys greater than the original key in BST.

Example:
```
Input: The root of a Binary Search Tree like this:
              5
            /   \
           2     13

Output: The root of a Greater Tree like this:
             18
            /   \
          20     13
```
## Solution
Use a global variable to store the sum and Inorder traverse.  
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
    public int sum = 0;
    public void traverse(TreeNode node){
        if(node.right != null){
            traverse(node.right);
        }
        sum += node.val;
        node.val = sum;
        if(node.left != null){
            traverse(node.left);
        }
    }
    public TreeNode convertBST(TreeNode root) {
        if(root == null){
            return root;
        }
        traverse(root);
        return root;
    }
}
```
