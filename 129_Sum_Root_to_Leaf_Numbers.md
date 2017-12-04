# Sum Root to Leaf Numbers
Given a binary tree containing digits from `0-9` only, each root-to-leaf path could represent a number.

An example is the root-to-leaf path `1->2->3` which represents the number `123`.

Find the total sum of all root-to-leaf numbers.

For example,
```
    1
   / \
  2   3
```
The root-to-leaf path `1->2` represents the number `12`.
The root-to-leaf path `1->3` represents the number `13`.

Return the sum = 12 + 13 = 25
## Solution
Backtracking.  
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
    int sum = 0;
    public void add(TreeNode t, int num){
        if(t == null) return ;
        num = num * 10 + t.val;
        if(t.left == null && t.right == null){
            sum += num;
            num = (num - t .val) / 10;
        }
        add(t.left, num);
        add(t.right, num);
        num = (num - t .val) / 10;
    }
    public int sumNumbers(TreeNode root) {
        add(root, 0);
        return sum;
    }
}
```
