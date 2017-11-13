# 117 Populating Next Right Pointers in Each Node II

### Problem

Follow up for problem "Populating Next Right Pointers in Each Node".

What if the given tree could be any binary tree? Would your previous solution still work?

Note:

You may only use constant extra space.
For example,
Given the following binary tree,
```
         1
       /  \
      2    3
     / \    \
    4   5    7
```
After calling your function, the tree should look like:
```
         1 -> NULL
       /  \
      2 -> 3 -> NULL
     / \    \
    4-> 5 -> 7 -> NULL
```

### Solutions

```java
/**
 * Definition for binary tree with next pointer.
 * public class TreeLinkNode {
 *     int val;
 *     TreeLinkNode left, right, next;
 *     TreeLinkNode(int x) { val = x; }
 * }
 */
public class Solution {
    public void connect(TreeLinkNode root) {
        if (root == null) {
            return;
        }
        TreeLinkNode node = root.next;
        TreeLinkNode next = null;
        while (node != null) {
            if (node.left != null) {
                next = node.left;
                break;
            }
            else if (node.right != null) {
                next = node.right;
                break;
            }
            else {
                node = node.next;
            }
        }
        if (root.left != null) {
            if (root.right != null) {
                root.left.next = root.right;
            }
            else {
                root.left.next = next;
            }
        }
        if (root.right != null) {
            root.right.next = next;
        }
        
        connect(root.right);
        connect(root.left);
    }
}
```