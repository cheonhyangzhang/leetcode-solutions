# 314 Binary Tree Vertical Order Traversal

### Problem:


Given a binary tree, return the vertical order traversal of its nodes' values. (ie, from top to bottom, column by column).

If two nodes are in the same row and column, the order should be from left to right.

Examples:

Given binary tree [3,9,20,null,null,15,7],
```
   3
  /\
 /  \
 9  20
    /\
   /  \
  15   7
```
return its vertical order traversal as:
```
[
  [9],
  [3,15],
  [20],
  [7]
]
```
Given binary tree [3,9,8,4,0,1,7],
```
     3
    /\
   /  \
   9   8
  /\  /\
 /  \/  \
 4  01   7
```

return its vertical order traversal as:
```
[
  [4],
  [9],
  [3,0,1],
  [8],
  [7]
]
```
Given binary tree [3,9,8,4,0,1,7,null,null,null,2,5] (0's right child is 2 and 1's left child is 5),
```
     3
    /\
   /  \
   9   8
  /\  /\
 /  \/  \
 4  01   7
    /\
   /  \
   5   2
```
return its vertical order traversal as:
```
[
  [4],
  [9,5],
  [3,0,1],
  [8,2],
  [7]
]
```

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
    public List<List<Integer>> verticalOrder(TreeNode root) {
        List<List<Integer>> left = new LinkedList<List<Integer>>();
        if (root == null) {
            return left;
        }
        List<List<Integer>> right = new LinkedList<List<Integer>>();
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        Queue<Integer> indexes = new LinkedList<Integer>();
        q.add(root);
        indexes.add(0);
        while (q.size() > 0) {
            TreeNode node = q.poll();
            int index = indexes.poll();
            if (index >= 0) {
                if (index >= right.size()) {
                    List<Integer> add = new LinkedList<Integer>();
                    add.add(node.val);
                    right.add(add);
                }
                else {
                    right.get(index).add(node.val);
                }
            }
            else {
                if (Math.abs(index) >= left.size() + 1) {
                List<Integer> add = new LinkedList<Integer>();
                add.add(node.val);
                left.add(0, add);
                }
                else {
                    left.get(left.size() - (Math.abs(index) - 1) - 1).add(node.val);
                }
            }
            if (node.left != null) {
                q.add(node.left);
                indexes.add(index - 1);
            }
            if (node.right != null) {
                q.add(node.right);
                indexes.add(index + 1);
            }
        }
        left.addAll(right);
        return left;
    }
}
```

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
    public List<List<Integer>> verticalOrder(TreeNode root) {
        List<List<Integer>> result = new LinkedList<List<Integer>>();
        if (root == null) {
            return result;
        }
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        Queue<Integer> indexes = new LinkedList<Integer>();
        HashMap<Integer, List<Integer>> cols = new HashMap<Integer, List<Integer>>();
        int min = Integer.MAX_VALUE;
        int max = Integer.MIN_VALUE;
        q.add(root);
        indexes.add(0);
        while (q.size() > 0) {
            TreeNode node = q.poll();
            int index = indexes.poll();
            min = Math.min(min, index);
            max = Math.max(max, index);
            if (!cols.containsKey(index)) {
                cols.put(index, new LinkedList<Integer>());
            }
            cols.get(index).add(node.val);
            if (node.left != null) {
                q.add(node.left);
                indexes.add(index - 1);
            }
            if (node.right != null) {
                q.add(node.right);
                indexes.add(index + 1);
            }
        }
        for (int i = min; i <=max; i ++) {
            if (cols.containsKey(i)) {
                result.add(cols.get(i));
            }
        }
        return result;
    }
}
```