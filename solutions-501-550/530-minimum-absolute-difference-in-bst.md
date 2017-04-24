# 530 Minimum Absolute Difference in BST

### Problem:

Given a binary search tree with non-negative values, find the minimum absolute difference between values of any two nodes.

Example:
```
Input:

   1
    \
     3
    /
   2

Output:
1

Explanation:
The minimum absolute difference is 1, which is the difference between 2 and 1 (or between 2 and 3).
```
Note: There are at least two nodes in this BST.

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
    public int getMinimumDifference(TreeNode root) {
        List<Integer> nums = new LinkedList<Integer>();
        inorder(root, nums);
        int min = Integer.MAX_VALUE;
        for (int i = 0; i < nums.size() - 1; i ++) {
            int cand = Math.abs(nums.get(i + 1) - nums.get(i));
            min = Math.min(min, cand);
        }
        return min;
    }
    private void inorder(TreeNode node, List<Integer> nums) {
        if (node == null) {
            return;
        }
        inorder(node.left, nums);
        nums.add(node.val);
        inorder(node.right, nums);
    }
}
```