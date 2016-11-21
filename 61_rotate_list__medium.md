# 61 Rotate List – Medium


### Problem:



Given a list, rotate the list to the right by k places, where k is non-negative.

For example:
Given 1->2->3->4->5->NULL and k = 2,
return 4->5->1->2->3->NULL.


### Thoughts:



Here we are going to use the approach that calculates the length of the list first, then get the offset and do the rotation.

If the input offset is always going to be valid, a fast and slow pointer way is a little better. But in the Leetcode version, k could be larger than the length, so we need the length anyway.


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
    public ListNode rotateRight(ListNode head, int k) {
        ListNode slow = head;
        ListNode fast = head;
        if (head == null) {
            return null;
        }
        ListNode tmp = head;
        int count = 0;
        while (tmp!= null) {
            tmp = tmp.next;
            count ++;
        }
        k = k % count;
        for (int i = 0; i < k ; i++) {
            fast = fast.next;
        }
        while(fast.next != null) {
            slow = slow.next;
            fast = fast.next;
        }
        fast.next = head;
        ListNode result = slow.next;
        slow.next = null;
        return result;
    }
}
```