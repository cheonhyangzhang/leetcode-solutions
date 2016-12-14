# 152 Sort List - Medium

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
    public ListNode sortList(ListNode head) {
        //return mergeSort(head);
        return quickSort(head);
    }
    private ListNode findMid(ListNode head) {
        ListNode slow = head;
        ListNode fast = head.next;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }
    private ListNode merge(ListNode left, ListNode right) {
        ListNode fakeHead = new ListNode(-1);
        ListNode p = fakeHead;
        while (left != null && right != null) {
            if (left.val < right.val) {
                p.next = left;
                left = left.next;
            }
            else {
                p.next = right;
                right = right.next;
            }
            p = p.next;
        }
        if (left != null) {
            p.next = left;
        }
        if (right != null) {
            p.next = right;
        }
        return fakeHead.next;
    }
    private ListNode mergeSort(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode mid = findMid(head);
        ListNode midNext = mid.next;
        mid.next = null;
        ListNode left = mergeSort(head);
        ListNode right = mergeSort(midNext);
        return merge(left, right);
    }
    
    private ListNode quickSort(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode left = new ListNode(-1);
        ListNode right = new ListNode(-1);
        ListNode mid = partition(left, right, head);
        left.next = quickSort(left.next);
        right.next = quickSort(right.next);
        return concat(left, right, mid);
    }
    private ListNode partition(ListNode left, ListNode right, ListNode head) {
        ListNode mid = head;
        ListNode l = left;
        ListNode r = right;
        ListNode p = head.next;
        while (p != null) {
            if (p.val <= head.val) {
                l.next = p;
                l = l.next;
            }
            else {
                r.next = p;
                r = r.next;
            }
            ListNode next = p.next;
            p.next = null;
            p = next;
        }
        mid.next = null;
        return mid;
    }
    private ListNode concat(ListNode left, ListNode right, ListNode mid) {
        ListNode fakeHead = new ListNode(-1);
        ListNode p = fakeHead;
        if (left.next != null) {
            p.next = left.next;
            p = getTail(left.next);
        }
        p.next = mid;
        p = mid;
        if (right.next != null) {
            p.next = right.next;
        }
        return fakeHead.next;
    }
    private ListNode getTail(ListNode head) {
        while (head.next != null) {
            head = head.next;
        }
        return head;
    }
    private int getLength(ListNode head) {
        int count = 0;
        while (head != null) {
            count ++;
            head = head.next;
        }
        return count;
    }
}
```