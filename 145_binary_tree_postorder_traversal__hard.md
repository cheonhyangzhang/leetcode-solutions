# 145 Binary Tree Postorder Traversal – Hard


### Problem:


Given a binary tree, return the postorder traversal of its nodes’ values.

For example:
Given binary tree {1,#,2,3},
1
\
2
/
3
return [3,2,1].

Note: Recursive solution is trivial, could you do it iteratively?

### Thoughts:


The key idea to solve trivial recursive problem is to properly leverage stack.
This makes sense because calling function recursively, behind the scene it’s using stack to keep track of the state of the program when function is called.

For this one, because postorder is root left right. So that when you have the root, you don’t want to add it to list yet, you want to expand it first.

So I am using another helper stack here to keep track if a node has been expanded.
If it hasn’t been expanded, don’t remove it from the stack. check the left and right child, if they are not null, push it to the stack, also the helper stack will push too, indicate these two children hasn’t been expanded. But the order here is check right first, because if we want to add left first, we need to push to stack later. Stack is First in last out.
If it has been expanded, remove it from the stack and add the val of the node to result list.


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
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> result = new LinkedList<Integer>();
        if (root == null) {
            return result;
        }
        Stack<TreeNode> s = new Stack<TreeNode>();
        Stack<Boolean> expand = new Stack<Boolean>();
        s.push(root);
        expand.push(true);
        while (s.size() > 0) {
            boolean exp = expand.pop();
            if (exp == true) {
                expand.push(false);
                TreeNode node = s.peek();
                if (node.right != null) {
                    s.push(node.right);
                    expand.push(true);
                }
                if (node.left != null) {
                    s.push(node.left);
                    expand.push(true);
                }
                continue;
            }
            result.add(s.pop().val);
        }
        return result;
    }
}
```