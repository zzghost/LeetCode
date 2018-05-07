# Serialize and Deserialize BST
## Description
Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary search tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary search tree can be serialized to a string and this string can be deserialized to the original tree structure.

**The encoded string should be as compact as possible.**  

**Note:** Do not use class member/global/static variables to store states. Your serialize and deserialize algorithms should be stateless.

## Solution
Use pre-order traversal to serialize the tree, use "#" to split the nodes.  
Deserialize: split the string with "#" and insert each node into the tree.  
**Complexity: Time O(logn).**  
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
public class Codec {

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        if(root == null){
            return "#";
        }
        Stack<TreeNode> stack = new Stack<>();
        TreeNode curr = root;
        stack.push(curr);
        //pre-order traversal.
        StringBuilder sb = new StringBuilder();
        while(!stack.empty()){
            TreeNode top = stack.pop();
            sb.append(String.valueOf(top.val));
            sb.append("#");
            if(top.right != null){
                stack.push(top.right);
            }
            if(top.left != null){
                stack.push(top.left);
            }
        }
        return sb.toString();
    }

    // Decodes your encoded data to tree.
    public void insert(TreeNode root, int value){
            if(root.val < value){
                if(root.right != null){
                    insert(root.right, value);
                }
                else{
                    root.right = new TreeNode(value);
                }
            }
            else{
                if(root.left != null){
                    insert(root.left, value);
                }
                else{
                    root.left = new TreeNode(value);
                }
            }

    }
    public TreeNode helper(String[] nodeVal){
        if(nodeVal == null || nodeVal.length == 0){
            return null;
        }
        TreeNode root = new TreeNode(Integer.parseInt(nodeVal[0]));
        for(int i = 1; i < nodeVal.length; i++){
            insert(root, Integer.parseInt(nodeVal[i]));
        }
        return root;
    }
    public TreeNode deserialize(String data) {
        String[] nodeVal = data.split("#");
        return helper(nodeVal);
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.deserialize(codec.serialize(root));
```
