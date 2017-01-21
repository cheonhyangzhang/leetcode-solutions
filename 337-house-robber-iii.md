# 337 House Robber III

### Problem:

<pre>
The thief has found himself a new place for his thievery again. There is only one entrance to this area, called the "root." Besides the root, each house has one and only one parent house. After a tour, the smart thief realized that "all houses in this place forms a binary tree". It will automatically contact the police if two directly-linked houses were broken into on the same night.

Determine the maximum amount of money the thief can rob tonight without alerting the police.

Example 1:
     3
    / \
   2   3
    \   \ 
     3   1
Maximum amount of money the thief can rob = 3 + 3 + 1 = 7.
Example 2:
     3
    / \
   4   5
  / \   \ 
 1   3   1
Maximum amount of money the thief can rob = 4 + 5 = 9.
</pre>

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
    private class Info {
        public int rob;
        public int norob;
        public Info(int rob, int norob) {
            this.rob = rob;
            this.norob = norob;
        }
    }
    public int rob(TreeNode root) {
        Info info = dfs(root);
        return Math.max(info.rob, info.norob);
    }
    private Info dfs(TreeNode node) {
        if (node == null) {
            return new Info(0, 0);
        }
        Info left = dfs(node.left);
        Info right = dfs(node.right);
        Info result = new Info(left.norob + right.norob + node.val, Math.max(left.rob, left.norob) + Math.max(right.rob, right.norob));
        return result;
    }
}
```