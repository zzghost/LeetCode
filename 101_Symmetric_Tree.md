# Symmetric Tree
## Description
Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree ``[1,2,2,3,4,4,3]`` is symmetric:
```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```
But the following ``[1,2,2,null,3,null,3]`` is not:
```
    1
   / \
  2   2
   \   \
   3    3
```
**Note:**  
Bonus points if you could solve it both recursively and iteratively.
## Solution
Depth-first traversal  
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
    public boolean solve(TreeNode p1, TreeNode p2){
        if(p1 == null && p2 == null) return true;
        if(p1 == null || p2 == null) return false;

        return p1.val == p2.val && solve(p1.left, p2.right) && solve(p1.right, p2.left);
    }
    public boolean isSymmetric(TreeNode root) {
        return solve(root, root);
    }
}
```
Non-recursive traversal: use two queues.  
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
    public boolean isSymmetric(TreeNode root) {
        Queue<TreeNode> q = new LinkedList<>();
        Queue<TreeNode> q2 = new LinkedList<>();
        q.offer(root); q2.offer(root);
        while(!q.isEmpty()){
            int size = q.size();
            for(int i = 0; i < size; i++){
                TreeNode tp1 = q.poll();
                TreeNode tp2 = q2.poll();
                if(tp1 == null && tp2 == null) continue;
                if(tp1 == null || tp2 == null) return false;
                if(tp1.val != tp2.val)
                    return false;
                q.offer(tp1.left);
                q2.offer(tp2.right);
                q.offer(tp1.right);
                q2.offer(tp2.left);

            }
        }
        return true;
    }
}
```
