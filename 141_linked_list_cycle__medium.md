# 141 Linked List Cycle – Medium


### Problem:



Given a linked list, determine if it has a cycle in it.

Follow up:
Can you solve it without using extra space?


### Thoughts:


A very classic problem to use two pointers.Slow fast pointers.  One pointer moves one forward each time and the other one moves two forward each time.

If there is a cycle, they will eventually meet. If there is no cycle, the faster pointer will meet null eventually.


### Solutions:



```java
/**
* Definition for singly-linked list.
* class ListNode {
* int val;
* ListNode next;
* ListNode(int x) {
* val = x;
* next = null;
* }
* }
*/
public class Solution {
    public boolean hasCycle(ListNode head) {
        if (head == null)
            return false;
        ListNode slower = head;
        ListNode faster = head.next;
        while ( slower != null && faster != null){
            if (slower == faster)
                return true;
            slower = slower.next;
            if (faster.next == null)
                break;
            faster = faster.next.next;
        }
        return false;
    }// hasCycle
}
```