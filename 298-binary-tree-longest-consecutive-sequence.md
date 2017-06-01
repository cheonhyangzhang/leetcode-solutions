# 298. Binary Tree Longest Consecutive Sequence

### Problem:

Given a binary tree, find the length of the longest consecutive sequence path.

The path refers to any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The longest consecutive path need to be from parent to child (cannot be the reverse).

For example,
```
   1
    \
     3
    / \
   2   4
        \
         5
```
Longest consecutive sequence path is 3-4-5, so return 3.
```
   2
    \
     3
    / 
   2    
  / 
 1
```
Longest consecutive sequence path is 2-3,not3-2-1, so return 2.

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
    private int result = 0;
    public int longestConsecutive(TreeNode root) {
        if (root == null) {
            return 0;
        }
        result = 0;
        lc(root);
        return result;
    }
    private int lc(TreeNode node) {
        if (node == null) {
            return 0;
        }
        int left = lc(node.left);
        int right = lc(node.right);
        int max = 1;
        if (node.left == null || node.left.val == node.val + 1) {
            max = Math.max(left + 1, max);
        }
        if (node.right == null || node.right.val == node.val + 1) {
            max = Math.max(right + 1, max);
        }
        result = Math.max(result, max);
        return max;
    }
}
```

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
    public int longestConsecutive(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int max = 0;
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        Queue<Integer> l = new LinkedList<Integer>();
        q.add(root);
        l.add(1);
        while (q.size() > 0) {
            TreeNode node = q.poll();
            int len = l.poll();
            max = Math.max(max, len);
            if (node.left != null) {
                if (node.left.val == node.val + 1) {
                    l.add(len + 1);
                }
                else {
                    l.add(1);
                }
                q.add(node.left);
            }
            if (node.right != null) {
                if (node.right.val == node.val + 1) {
                    l.add(len + 1);
                }
                else {
                    l.add(1);
                }
                q.add(node.right);
            }
        }
        return max;
    }
}
```