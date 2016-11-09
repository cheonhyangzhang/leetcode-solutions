# 86 Partition List – Medium


### Problem:



Given a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.

You should preserve the original relative order of the nodes in each of the two partitions.

For example,
Given 1->4->3->2->5->2 and x = 3,
return 1->2->2->4->3->5.


### Thoughts:



Use two pointers to keep two lists, one keep all elements that are less than given value and other keep elements that are greater or equal to give value.

Combine two lists in the end.


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
    public ListNode partition(ListNode head, int x) {
        ListNode lessHead = new ListNode(-1);
        ListNode moreHead = new ListNode(-1);
        ListNode less = lessHead;
        ListNode more = moreHead;
        ListNode node = head;
        while (node !=null ){
            if (node.val < x){
                less.next = node;
                less = less.next;
            }
            else{
                more.next = node;
                more = more.next;
            }
            node = node.next;
        }//while node
        more.next = null;
        less.next = moreHead.next;
        return lessHead.next;
    }//partition
}
```