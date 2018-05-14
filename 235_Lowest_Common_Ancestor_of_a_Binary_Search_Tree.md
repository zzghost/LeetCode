# Lowest Common Ancestor of a Binary Search Tree
## Description
Given a binary search tree (BST), find the lowest common ancestor (LCA) of two given nodes in the BST.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes v and w as the lowest node in T that has both v and w as descendants (where we allow a node to be a descendant of itself).”

Given binary search tree:  root = [6,2,8,0,4,7,9,null,null,3,5]
```
        _______6______
       /              \
    ___2__          ___8__
   /      \        /      \
   0      _4       7       9
         /  \
         3   5
```
Example 1:
```
Input: root, p = 2, q = 8
Output: 6
Explanation: The LCA of nodes 2 and 8 is 6.
```
Example 2:
```
Input: root, p = 2, q = 4
Output: 2
Explanation: The LCA of nodes 2 and 4 is 2, since a node can be a descendant of itself
             according to the LCA definition.
```

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
    public boolean preOrder(TreeNode curr, TreeNode target, ArrayList<TreeNode> path){
        path.add(curr);
        if(curr == target){
            return true;
        }
        if(curr == null && target != null){
            return false;
        }
        if(curr.val < target.val){
            return preOrder(curr.right, target, path);
        }
        else{
            return preOrder(curr.left, target, path);
        }
    }
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        ArrayList<TreeNode> pathP = new ArrayList<>();
        ArrayList<TreeNode> pathQ = new ArrayList<>();
        preOrder(root, p, pathP);
        preOrder(root, q, pathQ);
        TreeNode rst = null;
        for(int i = 0, j = 0; i < pathP.size() && j < pathQ.size(); i++, j++){
            if(pathP.get(i) == pathQ.get(j)){
                rst = pathP.get(i);
            }
        }
        return rst;
    }
}
```
