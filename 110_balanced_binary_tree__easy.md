# 110 Balanced Binary Tree – Easy


### Problem:



Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.


### Thoughts:



Check every node if they meet the criteria for balanced Binary Tree.  In order to do the check, we need the height of the left subtree and the right subtree of the current node.


### Solutions:


```java
/**
 * Definition for binary tree
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public boolean isBalanced(TreeNode root) {
        if (root == null) {
            return true;
        }
        return height(root) > 0;
    }
    private int height(TreeNode node) {
        if (node == null) {
            return 0;
        }
        int left = height(node.left);
        int right = height(node.right);
        if (left < 0 || right < 0 || Math.abs(left - right) > 1) {
            return -1;
        }
         
        return Math.max(left, right) + 1;
    }
}
```