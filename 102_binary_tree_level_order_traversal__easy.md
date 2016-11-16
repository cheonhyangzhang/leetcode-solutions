# 102 Binary Tree Level Order Traversal – Easy


### Problem:



Given a binary tree, return the level order traversal of its nodes’ values. (ie, from left to right, level by level).

For example:
Given binary tree {3,9,20,#,#,15,7},

    3
   / \
  9  20
    /  \
   15   7
return its level order traversal as:

[
  [3],
  [9,20],
  [15,7]
]

### Thoughts:


This is a bread first search order traversal.

Use two queues to remember which level currently at.


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
    public List<List<Integer>> levelOrder(TreeNode root) {
        Queue<TreeNode> qv = new LinkedList<TreeNode>();
        List<List<Integer>> result = new LinkedList<List<Integer>>();
        if (root == null) {
            return result;
        }
        qv.add(root);
        while (qv.size() > 0) {
            int n = qv.size();
            List<Integer> add = new LinkedList<Integer>();
            for (int i = 0; i < n; i ++) {
                TreeNode node = qv.remove();
                add.add(node.val);
                if (node.left !=null) {
                    qv.add(node.left);
                }
                if (node.right !=null) {
                    qv.add(node.right);
                }
            }
            result.add(add);
        }
        return result;
    }//list
}
```