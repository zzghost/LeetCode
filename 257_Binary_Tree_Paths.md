# Binary Tree Paths
## Description
Given a binary tree, return all root-to-leaf paths.

For example, given the following binary tree:
```
   1
 /   \
2     3
 \
  5
```
All root-to-leaf paths are:

["1->2->5", "1->3"]
## Solution
Depth-first Traversal.  
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
    List<String> rst = new ArrayList<>();
    List<String> onePath = new ArrayList<>();
    public void findPath(TreeNode curr){
        if(curr == null){
            return ;
        }
        onePath.add(String.valueOf(curr.val));
        if(curr.left == null && curr.right == null){
            rst.add(String.join("->", onePath));
            onePath.remove(onePath.size() - 1);
            return ;
        }
        findPath(curr.left);
        findPath(curr.right);
        onePath.remove(onePath.size() - 1);
    }
    public List<String> binaryTreePaths(TreeNode root) {
        findPath(root);
        return rst;
    }
}
```
