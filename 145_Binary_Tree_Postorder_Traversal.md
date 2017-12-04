# Binary Tree Postorder Traversal
## Description
Given a binary tree, return the postorder traversal of its nodes' values.

For example:
Given binary tree `{1,#,2,3}`,
```
  1
   \
    2
   /
  3
```
return `[3,2,1]`.

**Note:** Recursive solution is trivial, could you do it iteratively?
## Solution
1. Recursive
**Complexity: Time O(n), Space O(n)**
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
    public void postorder(TreeNode p){
        if(p == null) return ;
        postorder(p.left);
        postorder(p.right);
        rst.add(p.val);
    }
    public List<Integer> postorderTraversal(TreeNode root) {
        postorder(root);
        return rst;
    }
}
```
2. Non-Recursive  
Use stack.  
**Complexity: Time O(n), Space O(n)**
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
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> rst = new ArrayList<>();
        if(root == null) return rst;
        Stack<TreeNode> stack = new Stack<>();
        TreeNode p = root;
        while(!stack.isEmpty() || p != null){
            while(p != null){
                stack.push(p);
                rst.add(0, p.val);
                p = p.right;
            }
            TreeNode tp = stack.pop();
            p = tp.left;
        }
        return rst;
    }
}
```
