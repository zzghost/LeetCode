# Lowest Common Ancestor of a Binary Tree
## Description
Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to [the definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes v and w as the lowest node in T that has both v and w as descendants (where we allow a node to be a descendant of itself).”
```
        _______3______
       /              \
    ___5__          ___1__
   /      \        /      \
   6      _2       0       8
         /  \
         7   4
```
For example, the lowest common ancestor (LCA) of nodes 5 and 1 is 3. Another example is LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.


## Solution
Depth-first traversal twice and record the path respectively.  
Then traverse the path both at the same time.  
**Complexity: Time O(logn), Space O(logn).**  
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
    public void preOrder(TreeNode curr, TreeNode p, List<TreeNode> path){
        if(curr == null){
            return ;
        }
        if(!path.contains(p)){
            path.add(curr);
            preOrder(curr.left, p, path);
            preOrder(curr.right, p, path);
            if(!path.contains(p)){
                path.remove(path.size() - 1);
            }
        }
    }
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        List<TreeNode> pathP = new ArrayList<>(), pathQ = new ArrayList<>();
        preOrder(root, p, pathP);
        preOrder(root, q, pathQ);
        int len = (pathP.size() > pathQ.size()) ? pathQ.size() : pathP.size();
        TreeNode ancestor = null;
        for(int i = 0, j = 0; i < len && j < len; i++, j++){
            if(pathP.get(i) == pathQ.get(j)){
              //do not use `break` because we need lowest ancestor
                ancestor = pathP.get(i);
            }
        }
        return ancestor;
    }
}
```
