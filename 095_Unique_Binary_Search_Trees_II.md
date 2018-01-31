# Unique Binary Search Trees II
Given an integer n, generate all structurally unique BST's (binary search trees) that store values 1...n.

For example,
Given n = 3, your program should return all 5 unique BST's shown below.
```
   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```
## Solution
Dynamic Programming.  
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
    public TreeNode clone(TreeNode n, int offset){
        if(n == null) return n;
        TreeNode node = new TreeNode(n.val + offset);
        node.left = clone(n.left, offset);
        node.right = clone(n.right, offset);
        return node;
    }
    public List<TreeNode> generateTrees(int n) {
        List<TreeNode>[] rst = new List[n + 1];
        rst[0] = new ArrayList<>();
        if(n == 0) return rst[0];
        rst[0].add(null);
        for(int len = 1; len <= n; len++){
            rst[len] = new ArrayList<>();
            for(int j = 0; j < len; j++){
                for(TreeNode nodeL : rst[j]){
                    for(TreeNode nodeR : rst[len - j - 1]){
                        TreeNode node = new TreeNode(j + 1);
                        node.left = nodeL;
                        node.right = clone(nodeR, j + 1);
                        rst[len].add(node);
                    }
                }
            }
        }
        return rst[n];
    }
}
```
