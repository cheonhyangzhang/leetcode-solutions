# 147 Insertion Sort List – Medium


### Problem:



Sort a linked list using insertion sort.


### Thoughts:



This is a very basic sorting problem.

If you have learnt algorithms, this could be the very first algorithm you learnt.

Only difference is instead of an array, it is using a Single Linked List which complicates the problem a little bit. Because swapping two elements in a LinkedList is not that easy as in array.

The solution below is still in O(n^2) which is the standard insertion sort running time.


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
    public ListNode insertionSortList(ListNode head) {
        ListNode fakeHead = new ListNode(Integer.MIN_VALUE);
        while (head != null){
            ListNode p = fakeHead;
            while (p != null) {
                if ( head.val >= p.val && (p.next == null || head.val <= p.next.val)) {
                    ListNode next = head.next;
                    head.next = p.next;
                    p.next = head;
                    head = next;
                    break;
                }
                p = p.next;
            }
        }
        return fakeHead.next;
    }
}
```