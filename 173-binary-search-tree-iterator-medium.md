# 173 Binary Search Tree Iterator – Medium


### Problem:
Implement an iterator over a binary search tree (BST). Your iterator will be initialized with the root node of a BST.

Calling next() will return the next smallest number in the BST.

Note: next() and hasNext() should run in average O(1) time and uses O(h) memory, where h is the height of the tree.

### Thoughts:
Using a stack if helpful to implement the iterator.

Implementing iterator is like a inorder walk. which is left, root, right.

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
 
public class BSTIterator {
    Stack<TreeNode> helper = new Stack<TreeNode>();
    public BSTIterator(TreeNode root) {
        while (root != null) {
            helper.push(root);
            root = root.left;
        }
    }
 
    /** @return whether we have a next smallest number */
    public boolean hasNext() {
        return helper.size() != 0;
    }
 
    /** @return the next smallest number */
    public int next() {
        TreeNode result = helper.pop();
        TreeNode node = result.right;
        while (node != null) {
            helper.push(node);
            node = node.left;
        }
        return result.val;
    }
}
 
/**
 * Your BSTIterator will be called like this:
 * BSTIterator i = new BSTIterator(root);
 * while (i.hasNext()) v[f()] = i.next();
 */
```