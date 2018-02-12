# 671 Second Minimum Node In a Binary Tree

### Problem
Given a non-empty special binary tree consisting of nodes with the non-negative value, where each node in this tree has exactly two or zero sub-node. If the node has two sub-nodes, then this node's value is the smaller value among its two sub-nodes.

Given such a binary tree, you need to output the second minimum value in the set made of all the nodes' value in the whole tree.

If no such second minimum value exists, output -1 instead.

Example 1:
```
Input: 
    2
   / \
  2   5
     / \
    5   7

Output: 5
Explanation: The smallest value is 2, the second smallest value is 5.
```
Example 2:
```
Input: 
    2
   / \
  2   2

Output: -1
Explanation: The smallest value is 2, but there isn't any second smallest value.
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
    public int findSecondMinimumValue(TreeNode root) {
        if (root == null) {
            return -1;
        }
        int[] res = new int[1];
        res[0] = -1;
        preorder(root, root.val, res);
        return res[0];
    }
    private void preorder(TreeNode node, int min, int[] res) {
        if (node == null) {
            return;
        }
        if (node.val > min && (res[0] == -1 || node.val < res[0])) {
            res[0] = node.val;
        }
        preorder(node.left, min, res);
        preorder(node.right, min, res);
    }
}
```