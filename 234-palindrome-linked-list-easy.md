# 234 Palindrome Linked List – Easy

### Problem:
Given a singly linked list, determine if it is a palindrome.

Follow up:
Could you do it in O(n) time and O(1) space?

### Thoughts:
Given the limitation O(n) time and O(1) space, it makes things a little harder. Because it’s a singly linked list, so we can do it easily by reverse the list. But we cannot reverse the whole list because we need to compare. So we just need to reverse the second half and compare it in order with the first half.

Note that for 2->3, second half should start with 3 while for 2->3->4->6->5, second half should start with 6, when comparing, we only care about 2->3 and 5->6(reversed second half), we don’t need to care about 4.

To find the half of the singly list, we will need our old friend slow and fast pointer.

There is another solution that’s a little harder to come up with. It’s using recursion. Because we know that recursion of calling a function, Java will put the state of everything in stack, so leveraging recursion can be considered as using a Stack. We keep a “global” variable called left, then we create a recursion function that will leverage the state of the function. See the solutions below. isP function will be called on every node in the list, it will not do anything until it reaches the end of the list, when it passes the first two if, right is pointing to the last element of the list, while left is pointing to the first element of the list, so comparing them will determine the return value. But we need to move the left pointer to the next, because for the next, we will compare second element in the front and last second element in the back.
E.g. for 1->2->3->4, (here number is representing each node), the first compare is comparing 1 and 4, left is pointing to 1 and right is pointing to 4. When the function returns to upper level, right will be pointing to 3, that’s why we want to move left pointer so that it points to 2, next compare is 2 vs 3, and next will be 3 vs 2 and next will be 4 vs 1.

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
    public boolean isPalindrome(ListNode head) {
        if (head == null || head.next == null) {
            return true;
        }
        ListNode slow = head;
        ListNode fast = head.next;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        ListNode rev = reverse(slow.next);
        slow = head;
        fast = rev;
        while (fast != null) {
            if (slow.val != fast.val) {
                return false;
            }
            slow = slow.next;
            fast = fast.next;
        }
        return true;
    }
    private ListNode reverse(ListNode node) {
        ListNode reverse = new ListNode(-1);
        while (node != null) {
            ListNode next = node.next;
            node.next = reverse.next;
            reverse.next = node;
            node = next;
        }
        return reverse.next;
    }
}
```

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
    private ListNode left = null;
    public boolean isPalindrome(ListNode head) {
        if (head == null || head.next == null) {
            return true;
        }
        left = head;
        return isP(head);
    }
    private boolean isP(ListNode right) {
        if (right == null) {
            return true;
        }
        if (!isP(right.next)) {
            return false;
        }
        boolean result = left.val == right.val;
        left = left.next;
        return result;
    }
}
```