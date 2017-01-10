# 203 LeetCode Java: Remove Linked List Elements – Easy

### Problem:

Remove all elements from a linked list of integers that have value val.

Example
Given: 1 –> 2 –> 6 –> 3 –> 4 –> 5 –> 6, val = 6
Return: 1 –> 2 –> 3 –> 4 –> 5

### Thoughts;

This is a very simple linked list problem. Using a fakeHead is helping a lot for edge cases.

For many linked list problem, it’s always good practice to add a fakeHead in front in avoid null pointer problem in edge cases.

### Solutions:

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
/**
* Definition for singly-linked list.
* public class ListNode {
*     int val;
*     ListNode next;
*     ListNode(int x) { val = x; }
* }
*/
public class Solution {
    public ListNode removeElements(ListNode head, int val) {
        ListNode fakeHead = new ListNode(-1);
        fakeHead.next = head;
 
        ListNode parent = fakeHead;
        ListNode node = head;
        while (node != null){
            if (node.val == val)
                parent.next = node.next;
            else
                parent = node;
        node = node.next;
        }//while
        return fakeHead.next;
    }
}
``````java
Updated: 12/31/2016
Improve logic.

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
    public ListNode removeElements(ListNode head, int val) {
        ListNode fakeHead = new ListNode(-1);
        fakeHead.next = head;
        ListNode node = fakeHead;
        while (node.next != null) {
            if (node.next.val == val) {
                node.next = node.next.next;
            } 
            else {
                node = node.next;
            }
        }
        return fakeHead.next;
    }
}
```