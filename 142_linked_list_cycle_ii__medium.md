# 142 Linked List Cycle II – Medium


### Problem:



Given a linked list, return the node where the cycle begins. If there is no cycle, return null.

Note: Do not modify the linked list.

Follow up:
Can you solve it without using extra space?


### Thoughts:



The additional requirement is to return the beginning node of the cycle.

This is a very Mathy problem, don’t think it’s a good one for interview, unless your purpose is to test the person’s math skills.

Here is a little analysis:

If there is a cycle,

faster pointer travels a distance, while slower pointer travels b distance.

then we define from head to the begin node of the circle is c distance, and two pointers meet at offset d distance from the begin node, and the circle is X distance.

so that

a = c + k1 * X + d

b = c + k2 * X + d

and we have one additional equation

a = 2 * b

c + k1 * X + d = 2c + 2k2*X + 2d

(k1 – 2k2) * X = c + d

c = (k1 – 2k2) * X – d

so that after two pointers meet.

get a new pointer start from head, use this and faster pointer both travel one step each time,

when they meet, it’s the starting node.

Because for the faster pointer, it moves another c step, it equals X – d, which is the start node of the cycle.


### Solutions:



```java
/**
* Definition for singly-linked list.
* class ListNode {
*     int val;
*     ListNode next;
*     ListNode(int x) {
*        val = x;
*        next = null;
*     }
* }
*/
public class Solution {
    public ListNode detectCycle(ListNode head) {
        if (head == null)
            return null;
        ListNode slower = head;
        ListNode faster = head;
        while (slower != null && faster !=null){
            slower = slower.next;
            faster = faster.next;
            if (faster != null)
                faster = faster.next;
            if (slower == faster)
                break;
        }//while
        if (faster == null)
            return null;
        slower = head;
        while (slower != faster){
            slower = slower.next;
            faster = faster.next;
        }
        return slower;
    }//detectCycle
}
```