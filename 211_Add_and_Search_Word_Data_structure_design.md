# Add and Search Word - Data structure design
Design a data structure that supports the following two operations:
```
void addWord(word)
bool search(word)
```
search(word) can search a literal word or a regular expression string containing only letters a-z or .. A . means it can represent any one letter.

Example:
```
addWord("bad")
addWord("dad")
addWord("mad")
search("pad") -> false
search("bad") -> true
search(".ad") -> true
search("b..") -> true
```
Note:
You may assume that all words are consist of lowercase letters `a-z`.
## Solution
Use Trie Tree and Depth-First Search.  
```java
class WordDictionary {

    /** Initialize your data structure here. */
    class TrieNode{
        boolean isEnd = false;
        HashMap<Character, TrieNode> subNodes = new HashMap<>();
        TrieNode(){}
        boolean getKeywordEnd(){
            return isEnd;
        }
        void setKeywordEnd(boolean end){
            this.isEnd = end;
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

    public WordDictionary() {
        root = new TrieNode();
    }

    /** Adds a word into the data structure. */
    public void addWord(String word) {
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
                tmpNode.setKeywordEnd(true);
            }
        }
    }

    /** Returns if the word is in the data structure. A word could contain the dot character '.' to represent any one letter. */
    public boolean dfs(String word, int idx, TrieNode curr){
        if(idx == word.length()){
            return (curr.getKeywordEnd());
        }
        char c = word.charAt(idx);
        if(c == '.'){
            Iterator iter = curr.subNodes.entrySet().iterator();
            boolean rst = false;
            while(iter.hasNext()){
                Map.Entry entry = (Map.Entry)iter.next();
                TrieNode node = (TrieNode)entry.getValue();
                rst = rst || dfs(word, idx + 1, node);
            }
            return rst;
        }
        else{
            TrieNode node = curr.getSubNode(c);
            if(node == null){
                return false;
            }
            return dfs(word, idx + 1, node);
        }
    }
    public boolean search(String word) {
        TrieNode tmpNode = root;
        return dfs(word, 0, tmpNode);
    }
}

/**
 * Your WordDictionary object will be instantiated and called as such:
 * WordDictionary obj = new WordDictionary();
 * obj.addWord(word);
 * boolean param_2 = obj.search(word);
 */
```
