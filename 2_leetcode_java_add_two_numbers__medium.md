# 2 LeetCode Java: Add Two Numbers – Medium


### Problem:


You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8


### Thoughts:


This problem is given by an easy way. The numbers are stored reversely so that we could add from the left to right. The thing to keep in mind is that the two numbers might not have the same length.

The most clear way to handle this is to iterate over the two numbers list, iteration continues until reaches the end of the longer list. When the shorter list reaches the end already, consider the digit to be zero.


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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode n1 = l1;
        ListNode n2 = l2;
        ListNode fakeHead = new ListNode(-1);
        ListNode result = fakeHead;
        int toAdd = 0;
        while(!(n1 == null && n2 == null)){
            int v1 = 0;
            int v2 = 0;
            if (n1 != null){
                v1 = n1.val;
                n1 = n1.next;
            }
            if (n2 != null){
                v2 = n2.val;
                n2 = n2.next;
            }
            int tmp = v1 + v2 + toAdd;
            result.next = new ListNode(tmp % 10);
            result = result.next;
            toAdd = tmp / 10;
             
        }
        if (toAdd > 0){
            result.next = new ListNode(toAdd);
        }
        return fakeHead.next;
    }
}
```
One thing to notice about the above solution is that it have operation that is not quite necessary, line 27 – 30. Especially for test case, 0->1, 1->2->3->4->5->6->7->8->9. If one number is significantly longer, then there is no need to do the addition, module, and maybe not necessary the new node (if toAdd is 0 which means no more addition is needed). But if we stop looping when we meet the end of shorter list and re-point the tail to be the same position at the longer list, now we are modifying the original number list.

The notes above is just thoughts on the solution and other possibilities, just in case there are different requirements and constraints by the problem.