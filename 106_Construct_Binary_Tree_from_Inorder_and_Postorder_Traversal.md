#  Construct Binary Tree from Inorder and Postorder Traversal
## Description
Given inorder and postorder traversal of a tree, construct the binary tree.  

**Note:**
You may assume that duplicates do not exist in the tree.  
## Solution
Recursive.  
**Complexity : Time O(nlogn), Space O(n).**
```java
public TreeNode build(int[] inorder, int[] postorder, int inStart, int inEnd, int postStart, int postEnd, Map<Integer, Integer> map){
    if(postStart >= postEnd || postEnd > postorder.length)
        return null;
    int val = postorder[postEnd - 1];
    TreeNode node = new TreeNode(val);

    node.left = build(inorder, postorder, inStart, map.get(val), postStart, postStart + map.get(val) - inStart, map);
    node.right = build(inorder, postorder, map.get(val) + 1, inEnd, postStart + map.get(val) - inStart, postEnd - 1, map);
    return node;
}
public TreeNode buildTree(int[] inorder, int[] postorder) {
    Map<Integer, Integer> map = new HashMap<>();
    for(int i = 0; i < inorder.length; i++)
        map.put(inorder[i], i);
    return build(inorder, postorder, 0, inorder.length, 0, postorder.length, map);
}
```
