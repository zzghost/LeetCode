# Binary Tree Inorder Traversal
Given a binary tree, return the inorder traversal of its nodes' values.

For example:
Given binary tree `[1,null,2,3]`,
```
   1
    \
     2
    /
   3
```
return `[1,3,2]`.

**Note:** Recursive solution is trivial, could you do it iteratively?


## Solution
1. Recursive
**Complexity: Time O(n), Space O(n).**
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
    List<Integer> rst = new ArrayList<>();
    public void inorder(TreeNode p){
        if(p == null) return ;
        inorder(p.left);
        rst.add(p.val);
        inorder(p.right);
    }
    public List<Integer> inorderTraversal(TreeNode root) {
        inorder(root);
        return rst;
    }
}
```
2. Non-recursive  
Use stack.  
**Complexity: Time O(n), Space O(n).**
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
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> rst = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        TreeNode p = root;
        while(!stack.isEmpty() || p != null){
            while(p != null){
                stack.push(p);
                p = p.left;
            }
            TreeNode tp = stack.pop();
            rst.add(tp.val);
            p = tp.right;
        }
        return rst;
    }
}
```
