# 333 Largest BST Subtree

### Problem:

<pre>
Given a binary tree, find the largest subtree which is a Binary Search Tree (BST), where largest means subtree with largest number of nodes in it.

Note:
A subtree must include all of its descendants.
Here's an example:
    10
    / \
   5  15
  / \   \ 
 1   8   7
The Largest BST Subtree in this case is the highlighted one. 
The return value is the subtree's size, which is 3.
Hint:

You can recursively use algorithm similar to 98. Validate Binary Search Tree at each node of the tree, which will result in O(nlogn) time complexity.
Follow up:
Can you figure out ways to solve it with O(n) time complexity?
</pre>

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
    private class State {
        public boolean isBST;
        public int min;
        public int max;
        public int num;
        public State(boolean isBST, int min, int max, int num) {
            this.isBST = isBST;
            this.min = min;
            this.max = max;
            this.num = num;
        }
    }
    private int max = 0;
    public int largestBSTSubtree(TreeNode root) {
        max = 0;
        lbst(root);
        return max;
    }
    private State lbst(TreeNode node) {
        State result = null;
        if (node == null) {
            return result;
        }
        State left = lbst(node.left);
        State right = lbst(node.right);
        if ((left == null || (left.isBST && node.val > left.max)) && (right == null || (right.isBST && node.val < right.min))) {
            //A valid BST
            int newMin = left == null?node.val:left.min;
            int newMax = right == null?node.val:right.max;
            int newNum = (left == null?0:left.num) + (right == null?0:right.num) + 1;
            max = Math.max(max, newNum);
            return new State(true, newMin, newMax, newNum);
        }
        return new State(false, 0, 0, 0);
    }
}
```