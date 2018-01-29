# 653 Two Sum IV - Input is a BST
### Problem
Given a Binary Search Tree and a target number, return true if there exist two elements in the BST such that their sum is equal to the given target.

Example 1:
```
Input: 
    5
   / \
  3   6
 / \   \
2   4   7

Target = 9
Output: True
```

Example 2:
```
Input: 
    5
   / \
  3   6
 / \   \
2   4   7

Target = 28

Output: False
```

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
class Solution {
    public boolean findTarget(TreeNode root, int k) {
        HashSet<Integer> appr = new HashSet<Integer>();
        return inorder(root, k, appr);
    }
    private boolean inorder(TreeNode node, int k, HashSet<Integer> appr) {
        if (node == null) {
            return false;
        }
        if (inorder(node.left, k, appr)) {
            return true;
        }
        if (appr.contains(k - node.val)) {
            return true;
        }
        appr.add(node.val);
        if (inorder(node.right, k, appr)) {
            return true;
        }
        return false;
    }
}
```