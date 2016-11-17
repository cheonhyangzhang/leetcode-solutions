# 105 Construct Binary Tree from Preorder and Inorder Traversal – Medium


### Problem:



Given preorder and inorder traversal of a tree, construct the binary tree.

Note:
You may assume that duplicates do not exist in the tree.


### Thoughts:



The key idea is to get the recursive partition correctly.

Because preorder is root, left, right. So the first element is always going to be the root for current tree.

For each step, find the root first, then partition the problem into sub problem by calculating the new range.


### Solutions:


```java
/**
* Definition for binary tree
* public class TreeNode {
* int val;
* TreeNode left;
* TreeNode right;
* TreeNode(int x) { val = x; }
* }
*/
public class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        if (preorder == null || inorder == null || preorder.length == 0 || inorder.length == 0 || preorder.length != inorder.length) {
            return null;
        }
        HashMap<Integer, Integer> inmap = new HashMap<Integer, Integer>();
        for (int i = 0; i < inorder.length; i ++) {
            inmap.put(inorder[i], i);
        }
        return gt(preorder, inorder, 0, preorder.length - 1, 0, inorder.length - 1, inmap);
    }
    private TreeNode gt(int[] pre, int[] in, int prel, int prer, int inl, int inr, HashMap<Integer, Integer> inmap) {
        if (prel > prer) {
            return null;
        }
        TreeNode root = new TreeNode(pre[prel]);
        int rootIndex = inmap.get(pre[prel]);
        int leftnum = rootIndex - inl;
        TreeNode left = gt(pre, in, prel + 1, prel + 1 + leftnum - 1, inl, rootIndex - 1, inmap);
        TreeNode right = gt(pre, in, prel + leftnum + 1, prer, rootIndex + 1, inr, inmap);
        root.left = left;
        root.right = right;
        return root;
    }
} 
```