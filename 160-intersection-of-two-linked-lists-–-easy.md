# 160 Intersection of Two Linked Lists – Easy

### Problem:

Write a program to find the node at which the intersection of two singly linked lists begins.

For example, the following two linked lists:

A:          a1 → a2
                   ↘
                     c1 → c2 → c3
                   ↗            
B:     b1 → b2 → b3
begin to intersect at node c1.

Notes:

If the two linked lists have no intersection at all, return null.
The linked lists must retain their original structure after the function returns.
You may assume there are no cycles anywhere in the entire linked structure.
Your code should preferably run in O(n) time and use only O(1) memory.
### Thoughts:

The solution is made of tree steps.

1 Count the length of each list of the two.

2 Init two pointers to the head of the two list and move the longer one by offset of the difference between two lists’ length.

3 Move two pointers together forward and if they meet, that’s the intersection, otherwise, there is not intersection.

### Solutions:
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    private int getLength(ListNode node) {
        int count = 0;
        while (node!= null) {
            node = node.next;
            count ++;
        }
        return count;
    }
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        int lengthA = getLength(headA);
        int lengthB = getLength(headB);
        ListNode longer = headA;
        ListNode shorter = headB;
        if (lengthA < lengthB) {
            longer = headB;
            shorter = headA;
        }
        int diff = Math.abs(lengthA - lengthB);
        for (int i = 0; i < diff; i ++) {
            longer = longer.next;
        }
        while (longer != shorter) {
            longer = longer.next;
            shorter = shorter.next;
        }
        return longer;
    }
}
```
