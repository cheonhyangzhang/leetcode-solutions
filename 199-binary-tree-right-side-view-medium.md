# 199 Binary Tree Right Side View – Medium


### Problem:
Given a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

For example:
Given the following binary tree,
```
   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
```
You should return [1, 3, 4].

### Thoughts:
This is a modified BFS. Could be solved in other way as well.

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
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> result = new LinkedList<Integer>();
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        Queue<Integer> l = new LinkedList<Integer>();
        if (root == null) {
            return result;
        }
        q.add(root);
        l.add(1);
        while (q.size() > 0) {
            TreeNode node = q.poll();
            int level = l.poll();
            if (l.size() == 0 || l.peek() != level) {
                result.add(node.val);
            }
            if (node.left != null) {
                q.add(node.left);
                l.add(level + 1);
            }
            if (node.right != null) {
                q.add(node.right);
                l.add(level + 1);
            }
        }
        return result;
    }
}
```