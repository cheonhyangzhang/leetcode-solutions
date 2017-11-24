# 98 Validate Binary Search Tree 

### Problem

Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

The left subtree of a node contains only nodes with keys less than the node's key.
The right subtree of a node contains only nodes with keys greater than the node's key.
Both the left and right subtrees must also be binary search trees.
Example 1:
```
    2
   / \
  1   3
```
Binary tree [2,1,3], return true.
Example 2:
```
    1
   / \
  2   3
```
Binary tree [1,2,3], return false.

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
public class Solution {
    public boolean isValidBST(TreeNode root) {
        return validate(root, Integer.MIN_VALUE, Integer.MAX_VALUE);
    }
    public static boolean validate(TreeNode root, long min, long max) {
		if (root == null) {
			return true;
		}
		if (root.val < min || root.val > max){
		    return false;
		}
		// left subtree must be < root.val && right subtree must be > root.val
		return validate(root.left, min, (long)root.val - 1) && validate(root.right, (long)root.val + 1, max);
	}
}
```




