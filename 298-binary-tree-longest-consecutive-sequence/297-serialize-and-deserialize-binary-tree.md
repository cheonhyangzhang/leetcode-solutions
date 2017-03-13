# 297 Serialize and Deserialize Binary Tree

### Problem:

Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

For example, you may serialize the following tree
```
    1
   / \
  2   3
     / \
    4   5
```
as "[1,2,3,null,null,4,5]", just the same as how LeetCode OJ serializes a binary tree. You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.
Note: Do not use class member/global/static variables to store states. Your serialize and deserialize algorithms should be stateless.

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
public class Codec {

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        StringBuilder sb = new StringBuilder();
        if (root == null) {
            return "";
        }
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        q.add(root);
        while (!q.isEmpty()) {
            TreeNode node = q.poll();
            if (node == null) {
                sb.append("#,");
            }
            else {
                sb.append(node.val + ",");
                q.add(node.left);
                q.add(node.right);
            }
        }
        return sb.toString();
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        if (data.equals("")) {
            return null;
        }
        String[] nodes = data.split(",");
        TreeNode root = null;
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        for (int i = 0; i < nodes.length; i ++) {
            if (q.isEmpty()) {
                root = new TreeNode(Integer.parseInt(nodes[i]));
                q.add(root);
            }
            else {
                TreeNode left = null;
                TreeNode right = null;
                if (!nodes[i].equals("#")){
                    left = new TreeNode(Integer.parseInt(nodes[i]));
                    q.add(left);
                }
                if (!nodes[i + 1].equals("#")){
                    right = new TreeNode(Integer.parseInt(nodes[i + 1]));
                    q.add(right);
                }
                TreeNode parent = q.poll();
                parent.left = left;
                parent.right = right;
                i = i + 1;
            }
        }
        return root;
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.deserialize(codec.serialize(root));
```