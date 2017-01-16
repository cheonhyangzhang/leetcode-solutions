# 206 LeetCode Java: Reverse Linked List -Easy

### Problem:

Reverse a singly linked list.

### Thoughts:

Very simple and straight forward problem on pointer manipulation of linked list nodes.

### Solutions:

Recursion version:

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
    public ListNode reverseList(ListNode head) {
        ListNode fakeHead = new ListNode(-1);
        reverse(head, fakeHead);
        return fakeHead.next;
    }
    //reverse returns the tail of the reversed list
    private ListNode reverse(ListNode node, ListNode fakeHead){
        if (node == null)
            return fakeHead;
        else{
            ListNode tail = reverse(node.next, fakeHead);
            tail.next = node;
            node.next = null;
            return node;
        }
    }
}
```
Non-recursion version:

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
    public ListNode reverseList(ListNode head) {
        ListNode fakeHead = new ListNode(-1);
        ListNode node = head;
        while (node != null){
            ListNode nodeNext = node.next;
            node.next = fakeHead.next;
            fakeHead.next = node;
            node = nodeNext;
        }
        return fakeHead.next;
    }
}
```