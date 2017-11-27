# Binary Tree Level Order Traversal
## Description
Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

For example:
Given binary tree `[3,9,20,null,null,15,7]`,
```
    3
   / \
  9  20
    /  \
   15   7
```
return its level order traversal as:
```
[
  [3],
  [9,20],
  [15,7]
]
```
## Solution
1. Count each level
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
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> rst = new ArrayList<>();
        if(root == null)
            return rst;
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);
        while(q.size() != 0){
            int size = q.size();
            List<Integer> alist = new ArrayList<>();            
            for(int i = 0; i < size; i++){
                TreeNode tmp = q.poll();
                alist.add(tmp.val);
                if(tmp.left != null) q.offer(tmp.left);
                if(tmp.right != null) q.offer(tmp.right);
            }
            rst.add(new ArrayList<>(alist));
        }
        return rst;
    }
}
```
2. Use *Flag* node
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
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> rst = new ArrayList<>();
        if(root == null)
            return rst;
        Queue<TreeNode> q = new LinkedList<>();
        TreeNode flag = null;
        q.offer(root);
        q.offer(flag);
        List<Integer> alist = new ArrayList<>();
        while(q.size() != 1){
            TreeNode tmp = q.poll();
            if(tmp == flag){
                rst.add(new ArrayList<>(alist));
                q.offer(flag);
                alist = new ArrayList<>();
                continue;
            }
            alist.add(tmp.val);
            if(tmp.left != null)  q.offer(tmp.left);
            if(tmp.right != null)  q.offer(tmp.right);
        }
        rst.add(new ArrayList<>(alist));
        return rst;
    }
}
```
