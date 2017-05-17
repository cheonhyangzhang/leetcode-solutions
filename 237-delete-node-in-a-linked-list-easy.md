#  237 Delete Node in a Linked List – Easy


### Problem:
Write a function to delete a node (except the tail) in a singly linked list, given only access to that node.

Supposed the linked list is 1 -> 2 -> 3 -> 4 and you are given the third node with value 3, the linked list should become 1 -> 2 -> 4 after calling your function.

### Thoughts:
This one seems a little bit hard at first glance, maybe? But actually it has hint so obviously. Because the list is singly linked list, there is no way to access the previous node of the node that needs to be deleted. So we have to modify the val of the node. We have seen problems that require don’t modify val property of node, but don’t get stuck in it.

Another thing is that the node is except the tail, so there is not need to check node.next != null.

### Solutions:

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    public void deleteNode(ListNode node) {
        node.val = node.next.val;
        node.next = node.next.next;
    }
}
```