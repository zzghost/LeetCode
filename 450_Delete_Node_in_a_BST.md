# Delete Node in a BST
## Description
Given a root node reference of a BST and a key, delete the node with the given key in the BST. Return the root node reference (possibly updated) of the BST.

Basically, the deletion can be divided into two stages:

+ Search for a node to remove.  
+ If the node is found, delete the node.  

**Note:** Time complexity should be O(height of tree).

Example:
```
root = [5,3,6,2,4,null,7]
key = 3

    5
   / \
  3   6
 / \   \
2   4   7

Given key to delete is 3. So we find the node with value 3 and delete it.

One valid answer is [5,4,6,2,null,null,7], shown in the following BST.

    5
   / \
  4   6
 /     \
2       7

Another valid answer is [5,2,6,null,4,null,7].

    5
   / \
  2   6
   \   \
    4   7
```
## Solution
Recursive.  
Consider the two situations:   
1)the node only has left child or right child: replace the node with this only child.  
3)the node has both children: find its successor t, replace the node with t and delete t in the right subtree.  
**Complexity: Time O(logn).**  
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
    public TreeNode findSuccessor(TreeNode root){
        while(root.left != null){
            root = root.left;
        }
        return root;
    }
    public TreeNode deleteNode(TreeNode root, int key) {
        if(root == null){
            return root;
        }
        if(key == root.val){
            if(root.left != null && root.right != null){
                TreeNode successor = findSuccessor(root.right);
                root.val = successor.val;
                //delete the successor in the right sub-tree
                root.right = deleteNode(root.right, root.val);
            }
            else{
                root = (root.left != null) ? root.left : root.right;
            }
        }
        else if(key < root.val){
            root.left = deleteNode(root.left, key);
        }
        else{
            root.right = deleteNode(root.right, key);
        }
        return root;
    }
}
```
