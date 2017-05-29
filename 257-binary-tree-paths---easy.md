# 257 Binary Tree Paths - Easy

### Problem
Given a binary tree, return all root-to-leaf paths.

For example, given the following binary tree:

   1
 /   \
2     3
 \
  5
All root-to-leaf paths are:

["1->2->5", "1->3"]

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
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> result = new LinkedList<String>();
        process(root, "", result);
        return result;
    }
    private void process(TreeNode node, String curr, List<String> result) {
        if (node == null) {
            return;
        }
        String next = curr + "->" + node.val;
        if (node.left == null && node.right == null) {
            result.add(next.substring(2));
        }
        process(node.left, next, result);
        process(node.right, next, result);
    }
}
```