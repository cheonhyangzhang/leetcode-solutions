# 545 Boundary of Binary Tree

### Problem:
Given a binary tree, return the values of its boundary in anti-clockwise direction starting from root. Boundary includes left boundary, leaves, and right boundary in order without duplicate nodes.

Left boundary is defined as the path from root to the left-most node. Right boundary is defined as the path from root to the right-most node. If the root doesn't have left subtree or right subtree, then the root itself is left boundary or right boundary. Note this definition only applies to the input binary tree, and not applies to any subtrees.

The left-most node is defined as a leaf node you could reach when you always firstly travel to the left subtree if exists. If not, travel to the right subtree. Repeat until you reach a leaf node.

The right-most node is also defined by the same way with left and right exchanged.

Example 1
```
Input:
  1
   \
    2
   / \
  3   4

Ouput:
[1, 3, 4, 2]

Explanation:
The root doesn't have left subtree, so the root itself is left boundary.
The leaves are node 3 and 4.
The right boundary are node 1,2,4. Note the anti-clockwise direction means you should output reversed right boundary.
So order them in anti-clockwise without duplicates and we have [1,3,4,2].
```

Example 2
```
Input:
    ____1_____
   /          \
  2            3
 / \          / 
4   5        6   
   / \      / \
  7   8    9  10  
       
Ouput:
[1,2,4,7,8,9,10,6,3]

Explanation:
The left boundary are node 1,2,4. (4 is the left-most node according to definition)
The leaves are node 4,7,8,9,10.
The right boundary are node 1,3,6,10. (10 is the right-most node).
So order them in anti-clockwise without duplicate nodes we have [1,2,4,7,8,9,10,6,3].
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
public class Solution {
    public List<Integer> boundaryOfBinaryTree(TreeNode root) {
        if (root == null) {
            return new LinkedList<Integer>();
        }
        List<TreeNode> left = new LinkedList<TreeNode>();
        if (root.left == null) {
            left.add(root);
        }
        else {
            TreeNode node = root;
            while (node != null) {
                left.add(node);
                if (node.left != null) {
                    node = node.left;
                }
                else {
                    node = node.right;
                }
            }    
        }
        List<TreeNode> right = new LinkedList<TreeNode>();
        if (root.right == null) {
            right.add(root);
        }
        else {
            TreeNode node = root;
            while (node != null) {
                right.add(0, node);
                if (node.right != null) {
                    node = node.right;
                }
                else {
                    node = node.left;
                }
            }    
        }
        List<TreeNode> mid = new LinkedList<TreeNode>();
        inorder(root, mid);
        if (mid.size() > 0 && left.get(left.size() - 1) == mid.get(0)) {
            mid.remove(0);
        }
        if (mid.size() > 0 && mid.get(mid.size() - 1) == right.get(0)) {
            right.remove(0);
        }
        if (right.size() > 0 && right.get(right.size() - 1) == left.get(0)) {
            right.remove(right.size() - 1);
        }
        List<Integer> res = new LinkedList<Integer>();
        for (TreeNode n:left) {
            res.add(n.val);
        }
        for (TreeNode n:mid) {
            res.add(n.val);
        }
        for (TreeNode n:right) {
            res.add(n.val);
        }
        return res;
    }
    private void inorder(TreeNode node, List<TreeNode> mid) {
        if (node == null) {
            return;
        }
        if (node.left == null && node.right == null) {
            mid.add(node);
        }
        else {
            inorder(node.left, mid);
            inorder(node.right, mid);
        }
    }
}
```

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
    public List<Integer> boundaryOfBinaryTree(TreeNode root) {
        List<Integer> res = new LinkedList<Integer>();
        if (root == null) {
            return res;
        }
        res.add(root.val);
        left(root.left, res);
        right(root.right, res);
        return res;
    }
    private void left(TreeNode node, List<Integer> res) {
        if (node == null) {
            return;
        }
        res.add(node.val);
        if (node.left != null) {
            left(node.left, res);
            inorder(node.right, res);
        }
        else {
            left(node.right, res);
        }
    }
    private void right(TreeNode node, List<Integer> res) {
        if (node == null) {
            return;
        }
        if (node.right != null) {
            inorder(node.left, res);
            right(node.right, res);
        }
        else {
            right(node.left, res);
        }
        res.add(node.val);
    }
    private void inorder(TreeNode node, List<Integer> res) {
        if (node == null) {
            return;
        }
        if (node.left == null && node.right == null) {
            res.add(node.val);
        }
        else {
            inorder(node.left, res);
            inorder(node.right, res);
        }
    }
}
```