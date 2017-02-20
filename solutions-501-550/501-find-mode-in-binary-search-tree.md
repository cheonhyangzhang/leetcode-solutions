# 501 Find Mode in Binary Search Tree

### Problem:

Given a binary search tree (BST) with duplicates, find all the mode(s) (the most frequently occurred element) in the given BST.

Assume a BST is defined as follows:

The left subtree of a node contains only nodes with keys less than or equal to the node's key.
The right subtree of a node contains only nodes with keys greater than or equal to the node's key.
Both the left and right subtrees must also be binary search trees.
For example:
Given BST [1,null,2,2],

```
   1
    \
     2
    /
   2
```
return [2].

Note: If a tree has more than one mode, you can return them in any order.

Follow up: Could you do that without using any extra space? (Assume that the implicit stack space incurred due to recursion does not count).

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
    public int[] findMode(TreeNode root) {
        if (root == null) {
            return new int[0];
        }
        HashMap<Integer, Integer> count = new HashMap<Integer, Integer>();
        process(root, count);
        int max = 0;
        int length = 0;
        for (Integer val:count.keySet()) {
            if (count.get(val) == max) {
                length ++;
            }
            if (count.get(val) > max) {
                length = 1;
                max = count.get(val);
            }
        }
        int[] result = new int[length];
        int k = 0;
        for (Integer val:count.keySet()) {
            if (count.get(val) == max) {
                result[k++] = val;
            }
        }
        return result;
    }
    private void process(TreeNode root, HashMap<Integer, Integer> count) {
        if (root == null) {
            return;
        }
        if (!count.containsKey(root.val)) {
            count.put(root.val, 1);
        }
        else {
            count.put(root.val, count.get(root.val) + 1);
        }
        process(root.left, count);
        process(root.right, count);
    }
}
```