# Binary Tree Zigzag Level Order Traversal
## Description
Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).

For example:
Given binary tree `[3,9,20,null,null,15,7]`,
```
    3
   / \
  9  20
    /  \
   15   7
```
return its zigzag level order traversal as:
```
[
  [3],
  [20,9],
  [15,7]
]
```
## Solution
[jianzhiOffer 032](https://github.com/zzghost/jianzhiOffer/tree/master/Q32) has this problem too.  
Here's a more concise solution: use ArrayList's property:it can insert in the front.  
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
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> rst = new ArrayList<>();
        if(root == null)
            return rst;
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);
        boolean even = true;
        while(!q.isEmpty()){
            int size = q.size();
            List<Integer> alist = new ArrayList<>();
            for(int i = 0; i < size; i++){
                TreeNode tmp = q.poll();
                if(even)
                    alist.add(tmp.val);
                else
                //insert in the front
                    alist.add(0, tmp.val);
                if(tmp.left != null) q.offer(tmp.left);
                if(tmp.right != null) q.offer(tmp.right);
            }
            even = !even;
            rst.add(alist);
        }
        return rst;
    }
}
```
