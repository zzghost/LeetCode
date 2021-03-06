# Populating Next Right Pointers in Each Node
Given a binary tree
```
    struct TreeLinkNode {
      TreeLinkNode *left;
      TreeLinkNode *right;
      TreeLinkNode *next;
    }
```
Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL.

Initially, all next pointers are set to NULL.

**Note:**  

You may only use constant extra space.
You may assume that it is a perfect binary tree (ie, all leaves are at the same level, and every parent has two children).
For example,
Given the following perfect binary tree,
```
         1
       /  \
      2    3
     / \  / \
    4  5  6  7
  ```
After calling your function, the tree should look like:
```
         1 -> NULL
       /  \
      2 -> 3 -> NULL
     / \  / \
    4->5->6->7 -> NULL
    ```
## Solution
1. Level Order traversal.  
**Complexity: Time O(n), Space O(n).**
```java
/**
 * Definition for binary tree with next pointer.
 * public class TreeLinkNode {
 *     int val;
 *     TreeLinkNode left, right, next;
 *     TreeLinkNode(int x) { val = x; }
 * }
 */
public class Solution {
    public void connect(TreeLinkNode root) {
        if(root == null || root.left == null && root.right == null) return ;
        TreeLinkNode p = root;
        Queue<TreeLinkNode> queue = new LinkedList<>();
        queue.offer(p);
        while(!queue.isEmpty()){
            int size = queue.size();
            for(int i = 0; i < size; i++){
                TreeLinkNode tmp = queue.poll();
                if(tmp.left != null){
                    tmp.left.next = (tmp.right != null) ? tmp.right : null;
                    queue.offer(tmp.left);
                }

                if(tmp.right != null){
                    tmp.right.next = (tmp.next == null) ? null : tmp.next.left;
                    queue.offer(tmp.right);
                }
            }
        }
        return ;
    }
}
```
2. Two pointers.
**Complexity: Time O(n), Space O(1).**
```java
public class Solution {
    public void connect(TreeLinkNode root) {
        if(root == null || root.left == null && root.right == null)
            return ;
        TreeLinkNode pre = null, curr = root;
        while(curr.left != null){
            pre = curr;
            //each level
            while(curr != null){
                curr.left.next = curr.right;
                curr.right.next = (curr.next == null) ? null : curr.next.left;
                curr = curr.next;
            }
            curr = pre.left;
        }
    }
}
```
