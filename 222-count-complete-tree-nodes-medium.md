# 222 Count Complete Tree Nodes – Medium


### Problem:
Given a complete binary tree, count the number of nodes.

Definition of a complete binary tree from Wikipedia:
In a complete binary tree every level, except possibly the last, is completely filled, and all nodes in the last level are as far left as possible. It can have between 1 and 2h nodes inclusive at the last level h.

### Thoughts:
This problem is a little tricky.

Straight forward way is to count every single node, either a BFS, or a DFS.

I didn’t try it cause I think it should fail on running time, otherwise this problem will not make any sense.

Actually, it only costs h = logn time to calculate the height of the tree. ( n is the number of nodes.)

So the key point is to calculate what’s the offset of the last element which is in the last row.

I tried a binary search approach but didn’t succeed yet. I think BS would work here.

There is another working approach which is easier to understand.

Divide and conquer,

condition to test if a tree is complete tree it to test the depth of left-most node and the depth of right-most node. If they are the same, then it is a complete tree.

It’s always easy to calculate the number of nodes in a complete tree, 2^h – 1, where h is the height.

But if the two depth is not the same, then recursively solve the problem, which is divide, countNodes for the left subtree and the right subtree, sum up and plus 1.

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
    public int countNodes(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int left = leftDepth(root);
        int right = rightDepth(root);
        if (left == right) {
            return (1<<left) - 1;
        }
        return countNodes(root.left) + countNodes(root.right) + 1;
    }
    private int leftDepth(TreeNode node) {
        int count = 0; 
        while (node != null) {
            count ++;
            node = node.left;
        }
        return count;
    }
    private int rightDepth(TreeNode node) {
        int count = 0;
        while (node != null) {
            count ++;
            node = node.right;
        }
        return count;
    }
}
```