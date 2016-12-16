# 156 Binary Tree Upside Down – Medium

### Problem:
Given a binary tree where all the right nodes are either leaf nodes with a sibling (a left node that shares the same parent node) or empty, flip it upside down and turn it into a tree where the original right nodes turned into left leaf nodes. Return the new root.

For example:
Given a binary tree {1,2,3,4,5},
```
    1
   / \
  2   3
 / \
4   5
```
return the root of the binary tree [4,5,2,#,#,3,1].
```

   4
  / \
 5   2
    / \
   3   1
```
confused what “{1,#,2,3}” means? > read more on how binary tree is serialized on OJ.

### Thoughts

The key point here is that the tree is given by strict condition.
all the right nodes are either leaf nodes with a sibling (a left node that shares the same parent node) or empty

This means if a node has a right child, the right child will never has a subtree, or in another word, the right child will not have any children.

So the basic step we will need is to reorganize the pointer between a node, its left child (if there is) and the right child (if there is). If left child is not empty, we go down to recursively solve the problem.
Using this method, we need to make sure to clean the left and right pointer of current node, otherwise, the original root will keep having old values in its left and right pointer.

Also, there could be an iterative solution which will avoid to use stack when calling function recursively.
The key idea for this method is to always solve (assign the correct value for left and right pointer of) current node.
Say for the example above,
Step 1, assign correct left and right for 1, which is null for both.
Step 2, assign correct left and right for 2, which is 3 and 1.
Step 3, assign correct left and right for 4, which is 5 and 2,
etc.
And need to have two pointer to keep the value of above level.

There could also be a version to use a modified post order solution.
This is similar to the first solution – recursion. The difference is that if we want to re-assign pointer from top to down OR from bottom to up?

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
    public TreeNode upsideDownBinaryTree(TreeNode root) {
            if (root == null)
                return null;
            TreeNode left = root.left, right = root.right;
            if (left != null) {
                TreeNode ret = upsideDownBinaryTree(left);
                left.left = right;
                left.right = root;
                root.left = null;
                root.right = null;
                return ret;
            }
            return root;
    }
}
```
Iterative solutions:

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
    public TreeNode upsideDownBinaryTree(TreeNode root) {
           TreeNode node = root, left = null, right = null;  
           while (node != null) {
               TreeNode nextNode = node.left;
               node.left = left;
               left = node.right;
               node.right = right;
               right = node;
               node = nextNode;
           }
           return right;
    }
}
```