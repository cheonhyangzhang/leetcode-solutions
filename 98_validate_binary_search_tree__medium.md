# 98 Validate Binary Search Tree – Medium


### Problem:



Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

The left subtree of a node contains only nodes with keys less than the node’s key.
The right subtree of a node contains only nodes with keys greater than the node’s key.
Both the left and right subtrees must also be binary search trees.

### Thoughts:



We based on the rules, for each node we have a valid range for the value.

For the root, there is really no limitation.

Say if the root is 5, then all left subtree elements has to fall into the range of Integer.MIN_VALUE to 4

and all right subtree elements has to fall into the range of 6 to Integer.MAX_VALUE.

Basically, here the MIN and MAX value means there is no boundary on that side as far as the element is a valid integer.


### Solutions:


```java
/**
* Definition for a binary tree node.
* public class TreeNode {
* int val;
* TreeNode left;
* TreeNode right;
* TreeNode(int x) { val = x; }
* }
*/
public class Solution {
    public boolean isValidBST(TreeNode root) {
        return validate(root, Integer.MIN_VALUE, Integer.MAX_VALUE, false, false);
    }
    public static boolean validate(TreeNode root, int min, int max, boolean left, boolean right) {
        if (root == null) {
            return true;
        }
        if (left == true && root.val <= min){ 
            return false; 
        } 
        if (right == true && root.val >=max){
            return false;
        }
        return validate(root.left, min, root.val, left, true) && validate(root.right, root.val, max, true, right);
    }
}
```
Updated: 11/16/2016
Non-Recursion version

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
    public boolean isValidBST(TreeNode root) {
        Stack<TreeNode> stack = new Stack<TreeNode>();
        TreeNode node = root;
        int min = Integer.MIN_VALUE;
        boolean minSet = false;
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
            if (minSet == true && node.val <= min) {
                return false;
            }
            min = node.val;
            minSet = true;
            node = node.right;
        }
        return true;
    }
}
```