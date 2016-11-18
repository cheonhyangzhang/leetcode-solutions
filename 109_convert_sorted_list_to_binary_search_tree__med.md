# 109 Convert Sorted List to Binary Search Tree – Medium


### Problem:



Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.


### Thoughts:



This is similar to the Sorted Array version of the problem.

It’s easier for sorted array because we could always easily find the mid element.

But for a sorted list, we cannot visit element randomly, can only visit in order.

So here in order to make code clean and easy, we are pretending we could get the mid element.


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
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public TreeNode sortedListToBST(ListNode head) {
        ListNode p = new ListNode(-1);
        p.next = head;
        int count = 0;
        ListNode node = head;
        while (node!=null) {
            count ++;
            node = node.next;
        }
        return gt(p, 0, count - 1);
    }
    private TreeNode gt(ListNode p, int start, int end){
        if (start > end) {
            return null;
        }
        int mid = (start + end) / 2;
        TreeNode left = gt(p, start, mid - 1);
        TreeNode root = new TreeNode(p.next.val);
        p.next = p.next.next;
        TreeNode right = gt(p, mid + 1, end);
        root.left = left;
        root.right = right;
        return root;
    }
}
```