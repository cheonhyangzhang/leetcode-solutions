# 404 Sum of Left Leaves

### Problem
Find the sum of all left leaves in a given binary tree.

Example:
```
    3
   / \
  9  20
    /  \
   15   7
```

There are two left leaves in the binary tree, with values 9 and 15 respectively. Return 24.

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
    public int sumOfLeftLeaves(TreeNode root) {
        if (root == null) {
            return 0;
        }
        if (root.left == null) {
            return sumOfLeftLeaves(root.right);
        }
        else {
            int count = 0;
            if (root.left.left == null && root.left.right == null) {
                count += root.left.val;
            }
            else {
                count += sumOfLeftLeaves(root.left);
            }
            count += sumOfLeftLeaves(root.right);
            return count;
        }
    }
}
```