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
        if (head == null) {
            return null;
        }
        RandomListNode node = head;
        while (node != null) {
            RandomListNode copied = new RandomListNode(node.label);
            copied.next = node.next;
            node.next = copied;
            node = node.next.next;
        }
        node = head;
        while (node != null) {
            System.out.println(node.label);
            node = node.next;
        }
        
        RandomListNode res = head.next;
        node = head;
        while (node != null) {
            RandomListNode copied = node.next;
            if (node.random != null) {
                node.next.random = node.random.next;
            }
            node = node.next.next;
        }
        node = head;
        while (node != null) {
            RandomListNode copied = node.next;
            node.next = copied.next;
            node = copied.next;
            copied.next = node == null?null:node.next;
            
        }
        return res;
    }
}
```