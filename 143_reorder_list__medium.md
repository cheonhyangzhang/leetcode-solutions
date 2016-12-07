# 143 Reorder List – Medium


### Problem:


Given a singly linked list L: L0→L1→…→Ln-1→Ln,
reorder it to: L0→Ln→L1→Ln-1→L2→Ln-2→…

You must do this in-place without altering the nodes’ values.

For example,
Given {1,2,3,4}, reorder it to {1,4,2,3}.

### Thoughts


This problem can be easily solved by using HashMap, but due to the requirement, “do this in-place”.
So the plan is to complete in three steps.
1 Find the middle element of the list.
2 Do a reverse operation on the second half of the list.
3 Merge the first half and second half in a fashion that picks element from each in order.


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
    public void reorderList(ListNode head) {
        if (head == null || head.next == null) {
            return;
        }
        ListNode mid = findMid(head);
        ListNode head2 = reverse(mid.next);
        mid.next = null;
        merge(head, head2);
    }
    private ListNode merge(ListNode head1, ListNode head2) {
        ListNode fakeHead = new ListNode(-1);
        ListNode node = fakeHead;
        while (head1 != null && head2 != null) {
            node.next = head1;
            head1 = head1.next;
            node.next.next = head2;
            head2 = head2.next;
            node = node.next.next;
        }
        if (head1 != null) {
            node.next = head1;
        }
        if (head2 != null) {
            node.next = head2;
        }
        return fakeHead.next;
    }
    private ListNode reverse(ListNode head) {
        ListNode fakeHead = new ListNode(-1);
        fakeHead.next = head;
        ListNode node = head;
        ListNode next = null;
        while(node != null) {
            next = node.next;
            node.next = fakeHead.next;
            fakeHead.next = node;
            node = next;
        }
        head.next = null;
        return fakeHead.next;
    }
    private ListNode findMid(ListNode head) {
        ListNode slow = head, fast = head.next;
        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }
        return slow;
    }
}
```