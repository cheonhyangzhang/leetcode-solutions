# 111Minimum Depth of Binary Tree – Easy


### Problem:



Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.


### Thoughts:



This is a very typical BFS problem. It could also be solved by a DFS as well.

BFS has a better average performance on this problem.


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
    public int minDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        q.add(root);
        int count = 0;
        while (q.size() > 0) {
            int n = q.size();
            count ++;
            boolean end = false;
            for (int i = 0; i < n; i ++) {
                TreeNode node = q.remove();
                if (node.left == null && node.right == null) {
                    end = true;
                }
                if (node.left != null) {
                    q.add(node.left);
                }
                if (node.right != null) {
                    q.add(node.right);
                }
            }
            if (end == true) {
                break;
            }
        }
        return count;
    }
}
```