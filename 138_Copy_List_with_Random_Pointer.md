# Copy List with Random Pointer

## Description
A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a deep copy of the list.


## Solution
Use `HashMap` to store the position.  
Use `ArrayList` to store the nodes in the list in turn.  
**Complexity: Time O(n), Space O(n).** 
```java
/**
 * Definition for singly-linked list with a random pointer.
 * class RandomListNode {
 *     int label;
 *     RandomListNode next, random;
 *     RandomListNode(int x) { this.label = x; }
 * };
 */
public class Solution {
    public RandomListNode copyRandomList(RandomListNode head) {
        Map<RandomListNode, Integer> map = new HashMap<>();
        ArrayList<RandomListNode> nodes = new ArrayList<>();
        RandomListNode p = head;
        int i = 0;
        //traverse list
        while(p != null){
            nodes.add(new RandomListNode(p.label));
            map.put(p, i);
            p = p.next;
            i++;
        }
        nodes.add(null);
        p = head;
        i = 0;
        //traverse list again
        while(p != null){
            nodes.get(i).next = nodes.get(i + 1);
            if(p.random != null){
                int id = map.get(p.random);
                nodes.get(i).random = nodes.get(id);
            }
            p = p.next;
            i++;
        }
        return nodes.get(0);
    }
}
```
