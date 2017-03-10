# 272 Closest Binary Search Tree Value II

### Problem
Given a non-empty binary search tree and a target value, find k values in the BST that are closest to the target.

Note:
Given target value is a floating point.
You may assume k is always valid, that is: k ≤ total nodes.
You are guaranteed to have only one unique set of k values in the BST that are closest to the target.
Follow up:
Assume that the BST is balanced, could you solve it in less than O(n) runtime (where n = total nodes)?

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
public class Solution {
    public List<Integer> closestKValues(TreeNode root, double target, int k) {
        List<Integer> result = new LinkedList<Integer>();
        ArrayList<Integer> inorder = new ArrayList<Integer>();
        init(root, inorder);
        double min = Double.MAX_VALUE;
        int index = -1;
        for (int i = 0; i < inorder.size(); i ++) {
            double tmp = inorder.get(i);
            if (Math.abs(tmp - target) < min) {
                min = Math.abs(tmp - target);
                index = i;
            }
        }
        int i = index;
        int j = index;
        while (result.size() < k) {
            System.out.println("i = " + i + "j = " + j);
            if (i == j) {
                result.add(inorder.get(i));
                i --;
                j ++;
                continue;
            }
            double a = Double.MAX_VALUE;
            double b = Double.MAX_VALUE;
            if (i >= 0) {
                a = Math.abs(inorder.get(i) - target);
            }
            if (j< inorder.size()) {
                b = Math.abs(inorder.get(j) - target);
            }
            if (a < b) {
                result.add(inorder.get(i));
                i = i - 1;
            }
            else {
                result.add(inorder.get(j));
                j = j + 1;
            }
        }
        return result;
    }
    private void init(TreeNode root, ArrayList<Integer> inorder) {
        if (root == null) {
            return;
        }
        init(root.left, inorder);
        inorder.add(root.val);
        init(root.right, inorder);
    }
}
```

```java

```