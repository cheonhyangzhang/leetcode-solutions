# 19 Remove Nth Node From End of List – Easy


### Problem:



Given a linked list, remove the nth node from the end of list and return its head.

For example,

   Given linked list: 1->2->3->4->5, and n = 2.

   After removing the second node from the end, the linked list becomes 1->2->3->5.
Note:
Given n will always be valid.
Try to do this in one pass.


### Thoughts:



Do this in one pass is kind of misleading somehow. This problem is probably aimed to test fast and slow pointer concept. However, use two pointer to iterate. Is that really a one pass solution? Behind the scene it’s identical to a two pass solution. From the running time of view, there is really no difference between fast and slow pointer way or calculate the length of the list and then iterate again.


### Solutions:



Fast and slow pointer:

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 * int val;
 * ListNode next;
 * ListNode(int x) {
 * val = x;
 * next = null;
 * }
 * }
 */
public class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode fakeHead = new ListNode(-1);
        fakeHead.next = head;
        ListNode fast = fakeHead;
        ListNode slow = fakeHead;
        for (int i = 0; i < n; i ++){
            fast = fast.next;
        }
        while (fast.next!=null){
            slow = slow.next;
            fast = fast.next;
        }
        slow.next = slow.next.next; //because n is valid so that slow.next is gauranteed to be non-null
        return fakeHead.next;
    }
}
```
Calculate length and then iterate:

```java
/**
* Definition for singly-linked list.
* public class ListNode {
* int val;
* ListNode next;
* ListNode(int x) {
* val = x;
* next = null;
* }
* }
*/
public class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        int len = 0;
        ListNode tmp = head;
        while(tmp != null){
            tmp = tmp.next;
            len ++;
        }
        int toDe = len - n;
        ListNode fakeHead = new ListNode(-1);
        ListNode parent = fakeHead;
        parent.next = head;
        while (toDe > 0){
            parent = parent.next;
            toDe --;
        }
        parent.next = parent.next.next;
        return fakeHead.next;
    }//removeNthFromEnd
}//Solution
```