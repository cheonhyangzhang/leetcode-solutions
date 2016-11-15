# 92 Reverse Linked List II – Medium



### Problem:



Reverse a linked list from position m to n. Do it in-place and in one-pass.

For example:
Given 1->2->3->4->5->NULL, m = 2 and n = 4,

return 1->4->3->2->5->NULL.

Note:
Given m, n satisfy the following condition:
1 ≤ m ≤ n ≤ length of list.


### Thoughts:



Pointer modification. The best strategy to deal with linked list, pointer modification problem is to draw the data structure on a paper. Plus, be careful to take care of edge case. Adding a fake head is efficient to deal with edge cases most of the time.

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
    public ListNode reverseBetween(ListNode head, int m, int n) {
        if (head == null) {
            return head;
        }
        ListNode fakeHead = new ListNode(-1);
        fakeHead.next = head;
        ListNode mp = fakeHead;
        for (int i = 0; i < m - 1; i ++) {
            mp = mp.next;
        }
        //mp.next is the first element to be reversed
        ListNode rhead = mp;
        mp = mp.next;
        ListNode rtail = mp;
        ListNode next = null;
        for (int i = 0; i < n - m + 1; i ++) {
            next = mp.next;
            mp.next = rhead.next;
            rhead.next = mp;
            mp = next;
        }
        rtail.next = mp;
        return fakeHead.next;
    }
}
```