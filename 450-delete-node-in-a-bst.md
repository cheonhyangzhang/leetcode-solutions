# 450 Delete Node in a BST

### Problem
Given a root node reference of a BST and a key, delete the node with the given key in the BST. Return the root node reference (possibly updated) of the BST.

Basically, the deletion can be divided into two stages:

Search for a node to remove.
If the node is found, delete the node.
Note: Time complexity should be O(height of tree).

Example:
```
root = [5,3,6,2,4,null,7]
key = 3

    5
   / \
  3   6
 / \   \
2   4   7

Given key to delete is 3. So we find the node with value 3 and delete it.

One valid answer is [5,4,6,2,null,null,7], shown in the following BST.

    5
   / \
  4   6
 /     \
2       7

Another valid answer is [5,2,6,null,4,null,7].

    5
   / \
  2   6
   \   \
    4   7
```

### Solutions


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
class Solution {
    public TreeNode deleteNode(TreeNode root, int key) {
        TreeNode pre = null;
        TreeNode node = root;
        while (node != null) {
            if (node.val == key) {
                break;
            }
            pre = node;
            if (node.val > key) {
                node = node.left;
            }
            else {
                node = node.right;
            }
        }
        if (node == null) {
            return root;
        }
        if (pre == null) {
            return del(node);
        }
        if (pre.left == node) {
            pre.left = del(node);
        }
        else {
            pre.right = del(node);
        }
        return root;
    }
    private TreeNode del(TreeNode node) {
        if (node.left == null && node.right == null) {
            return null;
        }
        if (node.left == null) {
            return node.right;
        }
        if (node.right == null) {
            return node.left;
        }
        TreeNode pre = node;
        TreeNode curr = node.right;
        while (curr.left != null) {
            pre = curr;
            curr = curr.left;
        }
        node.val = curr.val;
        if (pre.left == curr) {
            pre.left = curr.right;
        }
        else {
            pre.right = curr.right;
        }
        return node;
    }
}
```