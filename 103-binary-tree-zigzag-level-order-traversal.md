# 103 Binary Tree Zigzag Level Order Traversal

### Problem
Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).

For example:
Given binary tree [3,9,20,null,null,15,7],
```
    3
   / \
  9  20
    /  \
   15   7
```
return its zigzag level order traversal as:
```
[
  [3],
  [20,9],
  [15,7]
]
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
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        Queue<TreeNode> q = new LinkedList<>();
        List<List<Integer>> res = new LinkedList<>();
        if (root == null) {
            return res;
        }
        q.add(root);
        int level = 0;
        while (!q.isEmpty()) {
            int size = q.size();
            List<Integer> add = new LinkedList<>();
            for (int i = 0; i < size; i ++) {
                TreeNode node = q.poll();
                if (level % 2 == 0) {
                    add.add(node.val);
                }
                else {
                    add.add(0, node.val);
                }
                if (node.left != null) {
                    q.add(node.left);
                }
                if (node.right != null) {
                    q.add(node.right);
                }
            }
            res.add(add);
            level ++;
        }
        return res;
    }
}
```