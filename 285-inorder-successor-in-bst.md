# 285 Inorder Successor in BST

### Problem:

Given a binary search tree and a node in it, find the in-order successor of that node in the BST.

Note: If the given node has no in-order successor in the tree, return null.

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
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        if (p.right != null) {
            TreeNode node = p.right;
            while (node.left != null) {
                node = node.left;
            }
            return node;
        }
        TreeNode node = root;
        TreeNode min = null;
        while (node != p && node != null) {
            if (node.val < p.val) {
                node = node.right;
            }
            else {
                min = node;
                node = node.left;
            }
        }
        return min;
    }
    
}
```