# Binary Tree Right Side View
## Description
Given a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

For example:
Given the following binary tree,
```
   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
 ```

You should return ``[1, 3, 4]``.
## Solution
Breadth-first traversal.  
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
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> rightNodes = new ArrayList<>();
        Queue<TreeNode> queue = new LinkedList<>();
        if(root == null){
            return rightNodes;
        }
        queue.offer(root);

        while(!queue.isEmpty()){
            int size = queue.size();
            for(int i = 0; i < size; i++){
                TreeNode tp = queue.poll();
                if(tp.left != null){
                    queue.offer(tp.left);
                }
                if(tp.right != null){
                    queue.offer(tp.right);
                }
                if(i == size - 1){
                    rightNodes.add(tp.val);
                }
            }
        }
        return rightNodes;
    }
}

```
