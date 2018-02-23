# 501 Find Mode in Binary Search Tree

### Problem:

Given a binary search tree (BST) with duplicates, find all the mode(s) (the most frequently occurred element) in the given BST.

Assume a BST is defined as follows:

The left subtree of a node contains only nodes with keys less than or equal to the node's key.
The right subtree of a node contains only nodes with keys greater than or equal to the node's key.
Both the left and right subtrees must also be binary search trees.
For example:
Given BST [1,null,2,2],

```
   1
    \
     2
    /
   2
```
return [2].

Note: If a tree has more than one mode, you can return them in any order.

Follow up: Could you do that without using any extra space? (Assume that the implicit stack space incurred due to recursion does not count).

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
    public int[] findMode(TreeNode root) {
        if (root == null) {
            return new int[0];
        }
        HashMap<Integer, Integer> count = new HashMap<Integer, Integer>();
        process(root, count);
        int max = 0;
        int length = 0;
        for (Integer val:count.keySet()) {
            if (count.get(val) == max) {
                length ++;
            }
            if (count.get(val) > max) {
                length = 1;
                max = count.get(val);
            }
        }
        int[] result = new int[length];
        int k = 0;
        for (Integer val:count.keySet()) {
            if (count.get(val) == max) {
                result[k++] = val;
            }
        }
        return result;
    }
    private void process(TreeNode root, HashMap<Integer, Integer> count) {
        if (root == null) {
            return;
        }
        if (!count.containsKey(root.val)) {
            count.put(root.val, 1);
        }
        else {
            count.put(root.val, count.get(root.val) + 1);
        }
        process(root.left, count);
        process(root.right, count);
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
    private int count = 0;
    private int max = 0;
    private Integer curr = null;
    public int[] findMode(TreeNode root) {
        if (root == null) {
            return new int[0];
        }
        count = 0;
        max = 0;
        curr = null;
        List<Integer> result = new LinkedList<Integer>();
        process(root, result);
        int[] res = new int[result.size()];
        for (int i = 0; i < res.length; i ++) {
            res[i] = result.get(i);
        }
        return res;
    }
    private void process(TreeNode root, List<Integer> result) {
        if (root == null) {
            return;
        }
        process(root.left, result);
        if (curr == null || root.val != curr) {
            curr = root.val;
            count = 1;
        }
        else {
            count ++;
        }
        
        if (count == max) {
            result.add(curr);
        }
        else if (count > max) {
            max = count;
            result.clear();
            result.add(curr);
        }
        process(root.right, result);
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
class Solution {
    int max = 0;
    int curr = Integer.MIN_VALUE;
    int count = 0;
    List<Integer> res = new LinkedList<>();
    public int[] findMode(TreeNode root) {
        countNode(root);
        
        int[] resArray = new int[res.size()];
        int index = 0;
        for (Integer ele:res) {
            resArray[index++] = ele;
        }
        return resArray;
    }
    private void countNode(TreeNode node) {
        if (node == null) {
            return;
        }
        countNode(node.left);
        if (node.val == curr) {
            count ++;
            
        }
        else {
            curr = node.val;
            count = 1;
        }
        if (count > max) {
            res.clear();
            max = count;
            res.add(node.val);
        }
        else if (count == max) {
            res.add(node.val);
        }
        countNode(node.right);
    }
}
```
