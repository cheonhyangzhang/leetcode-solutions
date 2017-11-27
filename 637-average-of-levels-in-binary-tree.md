# 637 Average of Levels in Binary Tree

### Problem
Given a non-empty binary tree, return the average value of the nodes on each level in the form of an array.

Example 1:
```
Input:
    3
   / \
  9  20
    /  \
   15   7
Output: [3, 14.5, 11]
```
Explanation:
The average value of nodes on level 0 is 3,  on level 1 is 14.5, and on level 2 is 11. Hence return [3, 14.5, 11].
Note:
The range of node's value is in the range of 32-bit signed integer.

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
    public List<Double> averageOfLevels(TreeNode root) {
        List<Double> res = new LinkedList<Double>();
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        if (root == null) {
            return res;
        }
        q.add(root);
        while (!q.isEmpty()) {
            int n = q.size();
            double sum = 0;
            for (int i = 0; i < n; i ++) {
                TreeNode node = q.poll();
                sum += (double)node.val;
                if (node.left != null) {
                    q.add(node.left);
                }
                if (node.right != null) {
                    q.add(node.right);
                }
            }
            res.add(sum/(double)n);
        }
        return res;
    }
}
```