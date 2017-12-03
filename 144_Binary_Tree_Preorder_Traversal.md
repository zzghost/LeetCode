# Binary Tree Preorder Traversal
Given a binary tree, return the preorder traversal of its nodes' values.

For example:  
Given binary tree `[1,null,2,3]`,
```
   1
    \
     2
    /
   3
```
return `[1,2,3]`.

**Note: **Recursive solution is trivial, could you do it iteratively?


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
    public void preorder(TreeNode p){
        if(p == null) return ;
        rst.add(p.val);
        preorder(p.left);
        preorder(p.right);
    }
    public List<Integer> preorderTraversal(TreeNode root) {
        preorder(root);
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
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> rst = new ArrayList<>();
        if(root == null) return rst;
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        while(!stack.isEmpty()){
            TreeNode tp = stack.pop();
            rst.add(tp.val);
            if(tp.right != null) stack.push(tp.right);
            if(tp.left != null) stack.push(tp.left);
        }
        return rst;
    }
}
```
