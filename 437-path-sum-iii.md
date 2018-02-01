# 437 Path Sum III

### Problem
You are given a binary tree in which each node contains an integer value.

Find the number of paths that sum to a given value.

The path does not need to start or end at the root or a leaf, but it must go downwards (traveling only from parent nodes to child nodes).

The tree has no more than 1,000 nodes and the values are in the range -1,000,000 to 1,000,000.

```
Example:

root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

      10
     /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1

Return 3. The paths that sum to 8 are:

1.  5 -> 3
2.  5 -> 2 -> 1
3. -3 -> 11
```

### Solutions
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
class Solution {
    public int pathSum(TreeNode root, int sum) {
        HashMap<Integer, Integer> sums = new HashMap<Integer, Integer>();
        sums.put(0, 1);
        int[] res = new int[1];
        process(root, res, 0, sum, sums);
        return res[0];
    }
    private void process(TreeNode node, int[] res, int currSum, int sum, HashMap<Integer, Integer> sums) {
        if (node == null) {
            return;
        }
        int newSum = currSum + node.val;
        if (sums.containsKey(newSum - sum)) {
            res[0] += sums.get(newSum - sum);
        }
        if (!sums.containsKey(newSum)) {
            sums.put(newSum, 0);
        }
        sums.put(newSum, sums.get(newSum) + 1);
        process(node.left, res, newSum, sum, sums);
        process(node.right, res, newSum, sum, sums);
        sums.put(newSum, sums.get(newSum) - 1);
    }
}
```