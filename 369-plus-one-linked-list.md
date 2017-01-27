# 369. Plus One Linked List

### Problem:

Given a non-negative integer represented as non-empty a singly linked list of digits, plus one to the integer.

You may assume the integer do not contain any leading zero, except the number 0 itself.

The digits are stored such that the most significant digit is at the head of the list.

Example:
```
Input:
1->2->3

Output:
1->2->4
```

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
    public ListNode plusOne(ListNode head) {
        ListNode fakeHead = new ListNode(0);
        fakeHead.next = head;
        carry(fakeHead);
        if (fakeHead.val != 0) {
            return fakeHead;
        }
        return fakeHead.next;
    }
    private int carry(ListNode node) {
        if (node == null) {
            return 1;
        }
        int next = carry(node.next);
        if (next == 0) {
            return 0;
        }
        int tmp = node.val + next;
        node.val = tmp % 10;
        return tmp / 10;
    }
}
```