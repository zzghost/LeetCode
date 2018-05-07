# Implement Trie (Prefix Tree)
## Description
Implement a trie with `insert`, `search`, and `startsWith` methods.

Note:
You may assume that all inputs are consist of lowercase letters `a-z`.

## Solution
```java
class Trie {

    /** Initialize your data structure here. */
    class TrieNode{
        boolean isEnd = false;
        HashMap<Character, TrieNode> subNodes = new HashMap<>();
        TrieNode(){   
        }
        void setKeyword(boolean end){
            isEnd = end;
        }
        boolean getKeyword(){
            return isEnd;
        }
        int countSubNodes(){
            return subNodes.size();
        }
        TrieNode getSubNode(char c){
            return subNodes.get(c);
        }
        void addSubNode(char c, TrieNode node){
            subNodes.put(c, node);
        }
    }
    TrieNode root = null;
    public Trie() {
        root = new TrieNode();
    }

    /** Inserts a word into the trie. */
    public void insert(String word) {
        TrieNode tmpNode = root;
        for(int i = 0; i < word.length(); i++){
            char c = word.charAt(i);
            TrieNode node = tmpNode.getSubNode(c);
            if(node == null){
                node = new TrieNode();
                tmpNode.addSubNode(c, node);
            }
            tmpNode = node;
            if(i == word.length() - 1){
                tmpNode.setKeyword(true);
            }
        }
    }

    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        TrieNode tmpNode = root;
        for(int i = 0; i < word.length(); i++){
            char c = word.charAt(i);
            TrieNode node = tmpNode.getSubNode(c);
            if(node == null){
                return false;
            }
            tmpNode = node;
        }
        return tmpNode.getKeyword();
    }

    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        TrieNode tmpNode = root;
        for(int i = 0; i < prefix.length(); i++){
            char c = prefix.charAt(i);
            TrieNode node = tmpNode.getSubNode(c);
            if(node == null){
                return false;
            }
            tmpNode = node;
        }
        return true;
    }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```
