# 94 Binary Tree Inorder Traversal – Medium


### Problem:



Given a binary tree, return the inorder traversal of its nodes’ values.

For example:
Given binary tree {1,#,2,3},

   1
    \
     2
    /
   3
return [1,3,2].

Note: Recursive solution is trivial, could you do it iteratively?


### Thoughts:



This is kind of a tricky question. The best way to do a tree traversal, no matter preorder, inorder or postorder, is to use recursion. But his question requires to use iterative.

The key idea is to leverage a stack and a current pointer.

For a inorder traversal, it’s left, root, right. So we should always print out the most left element first, then the root, the last the right.

So push left child into the stack as deeper as possible. When there is no more left child, print the top of the stack, and also go deeper to the left substring of the top element if it has left child.


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
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new LinkedList<Integer>();
        Stack<TreeNode> stack = new Stack<TreeNode>();
        TreeNode node = root;
        while (true) {
            if (node != null){
                stack.push(node);
                node = node.left;
                continue;
            }
            if (stack.size() == 0) {
                break;
            }
            node = stack.pop();
            result.add(node.val);
            node = node.right;
        }
        return result;
    }
}
```