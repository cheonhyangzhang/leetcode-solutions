# 129 Sum Root to Leaf Numbers – Medium


### Problem:



Given a binary tree containing digits from 0-9 only, each root-to-leaf path could represent a number.

An example is the root-to-leaf path 1->2->3 which represents the number 123.

Find the total sum of all root-to-leaf numbers.

For example,

    1
   / \
  2   3
The root-to-leaf path 1->2 represents the number 12.
The root-to-leaf path 1->3 represents the number 13.

Return the sum = 12 + 13 = 25.


### Thoughts:



This is a very basic recursion problem. Binary Tree iteration.


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
    public int sumNumbers(TreeNode root) {
        if (root == null) {
            return 0;
        }
        return sum(root, "");
    }
    private int sum(TreeNode root, String curr){
        if (root.left == null && root.right == null) {
            return Integer.parseInt(curr + root.val);
        }
        int sums = 0;
        if (root.left != null) {
            sums += sum(root.left, curr + root.val);
        }
        if (root.right != null) {
            sums += sum(root.right, curr + root.val);
        }
        return sums;
    }
}
```