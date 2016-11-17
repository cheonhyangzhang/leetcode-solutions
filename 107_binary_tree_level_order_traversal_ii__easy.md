# 107 Binary Tree Level Order Traversal II – Easy


### Problem:



Given a binary tree, return the bottom-up level order traversal of its nodes’ values. (ie, from left to right, level by level from leaf to root).

For example:
Given binary tree {3,9,20,#,#,15,7},

    3
   / \
  9  20
    /  \
   15   7
return its bottom-up level order traversal as:

[
  [15,7],
  [9,20],
  [3]
]

### Thoughts:



This is almost identical to version I. Only difference is the order of the level elements.


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
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        Queue<TreeNode> qv = new LinkedList<TreeNode>();
        List<List<Integer>> result = new LinkedList<List<Integer>>();
        if (root == null) {
            return result;
        }
        qv.add(root);
        while (qv.size() > 0) {
            List<Integer> add = new LinkedList<Integer>();
            int n = qv.size();
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
            result.add(0, add);
        }
        return result;
    }// level
}
```