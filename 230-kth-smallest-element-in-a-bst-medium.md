# 230 Kth Smallest Element in a BST – Medium

### Problem:
Given a binary search tree, write a function kthSmallest to find the kth smallest element in it.

Note: 
You may assume k is always valid, 1 ≤ k ≤ BST’s total elements.

Follow up:
What if the BST is modified (insert/delete operations) often and you need to find the kth smallest frequently? How would you optimize the kthSmallest routine?

### Thoughts:
The most straightforward solution would be inorder traverse of the BST. Because BST has the property that left < root < right. So that we want to get the most left first, with the help of using a stack, we get the smallest element, the second smallest element, the third …. until we get the kth smallest element. For this solution, the running time will be O(k).

But we can do better here by using extra space. This is a common trade off. Usually, when you use more space, you can save some time. With the help of a HashMap to store the number of nodes in a subset with a node as its root. So given the root of the tree, we calculate the number of nodes of the left subtree. If we are so lucky that the left subtree is already k – 1 nodes, then the root is the wannted element, kth smallest element. If not, but if we are still lucky that the left subtree is having more than k – 1 elements, then we can forget about the right subtree because the kth smallest element is in the left subtree. Also, because we already calculate the number of nodes in the left subtree and stored in the HashMap, for any further process, we don't need to calculate the number of nodes again.  This seems to be faster, but actually, by calculating all the codes in left subtree, say left subtree has m nodes. We have visited all of the m nodes, so running time would be O(m). And we know m is bigger than k in this case, so that this solution actually takes longer time than the inorder traverse.  But this one will be very efficient if the function is called multiple times with the same tree, because in the future, less calculation will be needed to find out the kth smallest element.
Note in the solution below, the HashMap is declared as variable of the class, this is going to be helpful when calling the method for multiple times, but if the tree has been modified, the solution might not be correct, because the HashMap keeps number of nodes for old nodes that can be outdated. But this solution is passing the Leetcode judge, so I guess that the test cases are not modifying the trees? I am not quite sure. In order to make it work even when trees are modified, we can declare the variable inside of the function kthSmallest and pass it in count so that for each call, it creates a new HashMap, but this kind of loses the purpose of leveraging a HashMap

I don't know a way to handle perfectly for the requirement – "What if the BST is modified (insert/delete operations) often and you need to find the kth smallest frequently? How would you optimize the kthSmallest routine?". Because we don't have access to the BST modified operations. This means whenever there is a modified operation to the BST, we don't know which part is modified, so that we cannot know what previous information we have can be used. This results in we need to re-calculate everything.

The only thing I can think of is to have two heap, one max heap which keeps the size of k and the other is a min heap which keeps the rest of the elements.
Whenever there is a new element, compare it with the kth smallest element, if the new element is smaller, add it into the max heap and remove the previous kth smallest element. Add the removed element to the min heap, etc.
But this also requires we need to know when and what is added to the tree or removed from the tree. So it's the same issue as above.

### Solutions:

In order traverse

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
    public int kthSmallest(TreeNode root, int k) {
        Stack<TreeNode> stack = new Stack<TreeNode>();
        TreeNode p = root;
        while (p!= null || stack.size() > 0) {
            if (p != null) {
                stack.push(p);
                p = p.left;
            }
            else {
                TreeNode node = stack.pop();
                k --;
                if (k == 0) {
                    return node.val;
                }
                p = node.right;
            }
        }
        return 0;
    }
}
```

HashMap way.
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
    private HashMap<TreeNode, Integer> counts = new HashMap<TreeNode, Integer>();
    public int kthSmallest(TreeNode root, int k) {
        // Assume root is never null.
        int left = count(root.left);
        if (left == k - 1) {
            return root.val;
        }
        if (left > k - 1) {
            return kthSmallest(root.left, k);
        }
        else {
            return kthSmallest(root.right, k - left - 1);
        }
 
    }
    private int count(TreeNode node) {
        if (node == null) {
            return 0;
        }
        if (counts.containsKey(node)) {
            return counts.get(node);
        }
        int c = count(node.left) + count(node.right) + 1;
        counts.put(node, c);
        return c;
    }
}
```