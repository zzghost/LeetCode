# Validate Binary Search Tree
Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

The left subtree of a node contains only nodes with keys less than the node's key.
The right subtree of a node contains only nodes with keys greater than the node's key.
Both the left and right subtrees must also be binary search trees.
Example 1:
```
    2
   / \
  1   3
```
Binary tree `[2,1,3]`, return true.
Example 2:
```
    1
   / \
  2   3
```
Binary tree `[1,2,3]`, return false.
# Solution
1. inOrder
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
    List<Integer> list = new ArrayList<>();
    public void inOrder(TreeNode p){
        if(p == null)
            return ;
        if(p.left != null)
            inOrder(p.left);
        list.add(p.val);
        if(p.right != null)
            inOrder(p.right);
    }
    public boolean isValidBST(TreeNode root) {
        inOrder(root);
        int n = list.size();
        for(int i = 0;i < n - 1; i++)
            if(list.get(i) >= list.get(i + 1))
                return false;
        return true;
    }
}
```
2. Recursive
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
    public boolean valid(TreeNode root, Integer minVal, Integer maxVal){
        if(root == null) return true;
        boolean isValid = ((minVal == null || root.val > minVal) && (maxVal == null || root.val < maxVal));
        return isValid && valid(root.left, minVal, root.val) && valid(root.right, root.val, maxVal);
    }
    public boolean isValidBST(TreeNode root) {
        if(root == null) return true;
        return valid(root, null, null);
    }
}
```
