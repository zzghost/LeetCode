# Construct Binary Tree from Preorder and Inorder Traversal
## Description
Given preorder and inorder traversal of a tree, construct the binary tree.  

**Note:**
You may assume that duplicates do not exist in the tree.  

## Solution
Recursive.  
Use `HashMap` to store `inorder` and its index can save finding time.  
**Complexity: Time O(nlogn), Space O(n).**

```java
public TreeNode build(int[] preorder, int[] inorder, int preStart, int inStart, int inEnd, Map<Integer, Integer> map){
    if(inStart > inEnd || preStart > preorder.length - 1)
        return null;
    int val = preorder[preStart];
    TreeNode root = new TreeNode(val);

    root.left = build(preorder, inorder, preStart + 1, inStart, map.get(val) - 1, map);
    root.right = build(preorder, inorder, map.get(val) + preStart + 1 - inStart, map.get(val) + 1, inEnd, map);

    return root;
}
public TreeNode buildTree(int[] preorder, int[] inorder) {
    Map<Integer, Integer> map = new HashMap<>();
    for(int i = 0; i < inorder.length; i++)
        map.put(inorder[i], i);
    return build(preorder, inorder, 0, 0, inorder.length - 1, map);
}
```
