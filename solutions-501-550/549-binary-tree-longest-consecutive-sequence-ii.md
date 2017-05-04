# 549 Binary Tree Longest Consecutive Sequence II

### Problem:
Given a binary tree, you need to find the length of Longest Consecutive Path in Binary Tree.

Especially, this path can be either increasing or decreasing. For example, [1,2,3,4] and [4,3,2,1] are both considered valid, but the path [1,2,4,3] is not valid. On the other hand, the path can be in the child-Parent-child order, where not necessarily be parent-child order.

Example 1:
```
Input:
        1
       / \
      2   3
Output: 2
Explanation: The longest consecutive path is [1, 2] or [2, 1].
```
Example 2:
```
Input:
        2
       / \
      1   3
Output: 3
Explanation: The longest consecutive path is [1, 2, 3] or [3, 2, 1].
```

Note: All the values of tree nodes are in the range of [-1e7, 1e7].

### Solutions:
```java
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
    private class Node {
        private int incr;
        private int decr;
        public Node() {
            incr = 0;
            decr = 0;
        }
    }
    public int longestConsecutive(TreeNode root) {
        int[] res = new int[1];
        res[0] = 0;
        process(root, res);
        return res[0];
    }
    private Node process(TreeNode node, int[] res) {
        if (node == null) {
            return new Node();
        }
        Node left = process(node.left, res);
        Node right = process(node.right, res);
        Node curr = new Node();
        int sum_incr = 1;
        int sum_decr = 1;
        if (node.left != null) {
            if (node.left.val == node.val - 1) {
                curr.decr = Math.max(curr.decr, left.decr + 1);
                sum_incr += left.decr + 1;
            }
            if (node.left.val == node.val + 1) {
                curr.incr = Math.max(curr.incr, left.incr + 1);
                sum_decr += left.incr + 1;
            }
        }
        if (node.right != null) {
            if (node.right.val == node.val - 1) {
                curr.decr = Math.max(curr.decr, right.decr + 1);
                sum_decr += right.decr + 1;
            }
            if (node.right.val == node.val + 1) {
                curr.incr = Math.max(curr.incr, right.incr + 1);
                sum_incr += right.incr + 1;
            }
        }
        res[0] = Math.max(res[0], Math.max(sum_incr, sum_decr));
        return curr;
    }
}
```