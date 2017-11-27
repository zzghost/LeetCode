# Path Sum II
## Description
Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

For example:
Given the below binary tree and `sum = 22`,
```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
```
return
```
[
   [5,4,11,2],
   [5,8,4,5]
]
```
## Solution
Depth-first traversal.
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
    List<List<Integer>> rst = new ArrayList<>();
    public void find(TreeNode current,int sum, List<Integer> alist){
        if(current == null)
            return ;
        alist.add(current.val);
        if(current.left == null && current.right == null && sum - current.val == 0){
            rst.add(new ArrayList<>(alist));
            alist.remove(alist.size() - 1);
            return ;
        }
        find(current.left, sum - current.val, alist);
        find(current.right, sum - current.val, alist);
        alist.remove(alist.size() - 1);
    }
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        List<Integer> alist = new ArrayList<>();
        find(root, sum, alist);
        return rst;   
    }
}
```
