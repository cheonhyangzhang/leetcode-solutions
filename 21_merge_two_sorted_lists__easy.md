# 21 Merge Two Sorted Lists – Easy


### Problem:



Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.


### Thoughts:



This is a very straightforward problem. Using a fakeHead pointer is solving a lot of troubles in many list problems. For this problem, you don’t have to use it. You could also solve the problem without using it.


### Solutions:



```java
/**
* Definition for singly-linked list.
* public class ListNode {
*         int val;
*         ListNode next;
*         ListNode(int x) {
*                 val = x;
*                 next = null;
*         }
* }
*/
public class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode fakeNode = new ListNode(-1);
        ListNode node = fakeNode;
        while (l1 != null && l2 != null){
            if (l1.val < l2.val){
                node.next = l1;
                l1 = l1.next;
                node = node.next;
            }//if
            else{
                node.next = l2;
                l2 = l2.next;
                node = node.next;
             }//else
        }//while l1 & l2
        if (l1 != null){
            node.next = l1;
        }
        else if (l2 != null){
            node.next = l2;
        }
        return fakeNode.next;
    }
}
```