# 144 Binary Tree Preorder Traversal – Medium


### Problem:



Given a binary tree, return the preorder traversal of its nodes’ values.

For example:
Given binary tree {1,#,2,3},

   1
    \
     2
    /
   3
return [1,2,3].

Note: Recursive solution is trivial, could you do it iteratively?


### Thoughts:



It is trivial to use recursion approach to solve this problem.

Preorder is to do a root, left, right.

Always append when meets a root. Then go deeper to the left subtree if got one.

Using a Stack is very helpful, which guaranteed all elements in the subtree will be appended prior to the right child.


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
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result= new LinkedList<Integer>();
        Stack<TreeNode> s = new Stack<TreeNode>();
        if (root == null) {
            return result;
        }
        s.push(root);
        while (s.size() > 0) {
            TreeNode node = s.pop();
            result.add(node.val);
            if (node.right != null) {
                s.push(node.right);
            }
            if (node.left != null) {
                s.push(node.left);
            }
        }
        return result;
    }
   
}
```