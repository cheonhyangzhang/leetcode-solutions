# 101 Symmetric Tree – Easy


### Problem:



Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree is symmetric:

    1
   / \
  2   2
 / \ / \
3  4 4  3
But the following is not:

    1
   / \
  2   2
   \   \
   3    3
Note:
Bonus points if you could solve it both recursively and iteratively.


### Thoughts:



This is very similar to the Same Tree problem. Very straight forward in recursion way.


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
    public boolean isSymmetric(TreeNode root) {
        if (root == null) {
            return true;
        }
        // return recursion(root.left, root.right);
        return iterative(root);
    }
    private boolean recursion(TreeNode left, TreeNode right) {
        if (left == null && right == null) {
            return true;
        }
        if (left != null && right != null && left.val == right.val) {
            return recursion(left.left, right.right) && recursion(left.right, right.left);
        }
        return false;
    }
    private boolean iterative(TreeNode root) {
        Stack<TreeNode> left = new Stack<TreeNode>();
        Stack<TreeNode> right = new Stack<TreeNode>();
        left.push(root.left);
        right.push(root.right);
        while (left.size() > 0) {
            TreeNode l = left.pop();
            TreeNode r = right.pop();
            if (l == null && r == null) {
                continue;
            }
            if (l != null && r != null && l.val == r.val) {
                left.push(l.left);
                right.push(r.right);
                left.push(l.right);
                right.push(r.left);
                continue;
            }
            return false;
        }
        return true;
    }
}
```