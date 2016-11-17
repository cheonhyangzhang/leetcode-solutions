# 24 Swap Nodes in Pairs – Medium


### Problem:



Given a linked list, swap every two adjacent nodes and return its head.

For example,
Given 1->2->3->4, you should return the list as 2->1->4->3.

Your algorithm should use only constant space. You may not modify the values in the list, only nodes itself can be changed.


### Thoughts:



Very basic iteration of the list.

### Solutions:



```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 * int val;
 * ListNode next;
 * ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    public ListNode swapPairs(ListNode head) {
        ListNode fakeHead = new ListNode(-1);
        fakeHead.next = head;
        ListNode node = fakeHead;
        while (node!=null & node.next != null && node.next.next!= null){
            ListNode first = node;
            ListNode second = node.next;
            ListNode third = node.next.next;
            first.next = third;
            second.next = third.next;
            third.next = second;
            node = second;
        }
        return fakeHead.next;
    }
}
```