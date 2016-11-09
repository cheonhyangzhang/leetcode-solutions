# 82 LeetCode Java: Remove Duplicates from Sorted List II – Medium

### Problem:



Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.

For example,
Given 1->2->3->3->4->4->5, return 1->2->5.
Given 1->1->1->2->3, return 2->3.


### Thoughts:



The difference comparing to the version I is that instead of keeping the duplicate elements, removing all occurrence of duplicate elements.

Having a fakeHead is most of time a good practice to handle edge cases.


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
    public ListNode deleteDuplicates(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode fakeHead = new ListNode(-1);
        fakeHead.next = head;
        ListNode it = fakeHead;
        while (it.next != null && it.next.next != null) {
            if (it.next.val == it.next.next.val) {
                int val = it.next.val;
                while (it.next != null && it.next.val == val) {
                    it.next = it.next.next;
                }
            }
            else {
                it = it.next;
            }
        }
        return fakeHead.next;
    }
}
```