# 138 Copy List with Random Pointer

### Problem
A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a deep copy of the list.



### Solutions
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
        HashMap<RandomListNode, RandomListNode> map = new HashMap<>();
        RandomListNode original = head;
        while (original != null) {
            RandomListNode node = new RandomListNode(original.label);
            map.put(original, node);
            original = original.next;
        }
        original = head;
        while (original != null) {
            RandomListNode copied = map.get(original);
            copied.next = map.get(original.next);
            copied.random = map.get(original.random);
            original = original.next;
        }
        return map.get(head);
    }
}
```