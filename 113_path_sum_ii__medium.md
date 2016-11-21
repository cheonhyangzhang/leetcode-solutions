# 113 Path Sum II – Medium


### Problem:



Given a binary tree and a sum, find all root-to-leaf paths where each path’s sum equals the given sum.

For example:
Given the below binary tree and sum = 22,

              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
return

[
   [5,4,11,2],
   [5,8,4,5]
]

### Thoughts:



The only addition comparing to the version I of this problem is that instead of returning a boolean value, we need to have the exact path of numbers that has the given sum.

Approach will be very similar but need a ArrayList to keep current potential solution.


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
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        List<List<Integer>> result = new LinkedList<List<Integer>>();
        process(root, sum, new LinkedList<Integer>(), result);
        return result;
    }
    private void process(TreeNode node, int sum, List<Integer> curr, List<List<Integer>> result){
        if (node == null) {
            return;
        }
        curr.add(node.val);
        if (node.left == null && node.right == null & node.val == sum) {
            result.add(new LinkedList<Integer>(curr));
        }
        process(node.left, sum - node.val, curr, result);
        process(node.right, sum - node.val, curr, result);
        curr.remove(curr.size() - 1);
    }
}

```