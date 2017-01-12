# 270. Closest Binary Search Tree Value  

### Problem:

Given a non-empty binary search tree and a target value, find the value in the BST that is closest to the target.

Note:
Given target value is a floating point.
You are guaranteed to have only one unique value in the BST that is closest to the target.

# Solutions:

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
    private double min = 0;
    private int cand = 0;
    public int closestValue(TreeNode root, double target) {
        min = Double.MAX_VALUE;
        cand = 0;
        cv(root, target);
        return cand;
    }
    private void cv(TreeNode node, double target) {
        if (node == null) {
            return;
        }
        double diff = Math.abs(node.val - target);
        if (diff < min) {
            min = diff;
            cand = node.val;
        }
        if (target > node.val) {
            cv(node.right, target);
        }
        else {
            cv(node.left, target);
        }
    }   
}
```