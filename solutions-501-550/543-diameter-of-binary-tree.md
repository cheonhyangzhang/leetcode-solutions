# 543 Diameter of Binary Tree

### Problem:
Given a binary tree, you need to compute the length of the diameter of the tree. The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.

Example:
Given a binary tree 
```
          1
         / \
        2   3
       / \     
      4   5   
```
Return 3, which is the length of the path [4,2,1,3] or [5,2,1,3].

Note: The length of path between two nodes is represented by the number of edges between them.

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
    public int diameterOfBinaryTree(TreeNode root) {
        int[] res = new int[1];
        res[0] = 0;
        process(root, res);
        return res[0];
    }
    private int process(TreeNode node, int[] res) {
        if (node == null) {
            return -1;
        }
        int left = process(node.left, res) + 1;
        int right = process(node.right, res) + 1;
        res[0] = Math.max(res[0], left + right);
        return Math.max(left, right);
    }
}
```