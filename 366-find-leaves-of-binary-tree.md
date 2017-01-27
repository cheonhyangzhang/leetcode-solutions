# 366 Find Leaves of Binary Tree

### Problem:

Given a binary tree, collect a tree's nodes as if you were doing this: Collect and remove all leaves, repeat until the tree is empty.

Example:
Given binary tree 
<pre>
          1
         / \
        2   3
       / \     
      4   5    
</pre>

Returns [4, 5, 3], [2], [1].

Explanation:
1 Removing the leaves [4, 5, 3] would result in this tree:
<pre>
          1
         / 
        2     
</pre>
     
2 Now removing the leaf [2] would result in this tree:
<pre>
          1          
</pre>

3 Now removing the leaf [1] would result in the empty tree:
<pre>
          []         
</pre>


Returns [4, 5, 3], [2], [1].

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
    public List<List<Integer>> findLeaves(TreeNode root) {
        List<List<Integer>> result = new LinkedList<List<Integer>>();
        dfs(result, root);
        return result;
    }
    private int dfs(List<List<Integer>> result, TreeNode node) {
        if (node == null) {
            return 0;
        }
        int left = dfs(result, node.left);
        int right = dfs(result, node.right);
        int curr = Math.max(left, right) + 1;
        if (result.size() < curr) {
            result.add(new LinkedList());
        }
        result.get(curr - 1).add(node.val);
        return curr;
    }
}
```
