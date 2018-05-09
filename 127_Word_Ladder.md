# Word Ladder
## Description
Given two words (beginWord and endWord), and a dictionary's word list, find the length of shortest transformation sequence from beginWord to endWord, such that:

Only one letter can be changed at a time.
Each transformed word must exist in the word list. Note that beginWord is not a transformed word.
**Note:**

+ Return 0 if there is no such transformation sequence.
+ All words have the same length.
+ All words contain only lowercase alphabetic characters.
+ You may assume no duplicates in the word list.
+ You may assume beginWord and endWord are non-empty and are not the same.  

**Example 1:**
```
Input:
beginWord = "hit",
endWord = "cog",
wordList = ["hot","dot","dog","lot","log","cog"]

Output: 5

Explanation: As one shortest transformation is "hit" -> "hot" -> "dot" -> "dog" -> "cog",
return its length 5.
```
**Example 2:**  
```
Input:
beginWord = "hit"
endWord = "cog"
wordList = ["hot","dot","dog","lot","log"]

Output: 0

Explanation: The endWord "cog" is not in wordList, therefore no possible transformation.
```
## Solution
Breadth-First Search
```java
class Solution {
    class node{
        String word;
        int count;
        node(String word, int count){
            this.word = word;
            this.count = count;
        }
    }
    public boolean differOne(String str1, String str2){
        int count = 0;
        for(int i = 0; i < str1.length(); i++){
            if(str1.charAt(i) != str2.charAt(i)){
                count++;
            }
        }
        return count <= 1;
    }
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        if(beginWord.equals(endWord)){
            return 0;
        }
        Queue<node> queue = new LinkedList<>();
        queue.offer(new node(beginWord, 1));
        while(!queue.isEmpty()){
            node top = queue.poll();
            if(top.word.equals(endWord)){
                return top.count;
            }
            int i = 0;
            while(i < wordList.size()){
                if(differOne(top.word, wordList.get(i))){
                    queue.offer(new node(wordList.get(i), top.count + 1));
                    //ensure each word is changed exactly once
                    wordList.remove(i);
                }
                else{
                    i++;
                }
            }  
        }
        return 0;
    }
}
```
