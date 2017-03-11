# 272 Closest Binary Search Tree Value II

### Problem
Given a non-empty binary search tree and a target value, find k values in the BST that are closest to the target.

Note:
Given target value is a floating point.
You may assume k is always valid, that is: k ≤ total nodes.
You are guaranteed to have only one unique set of k values in the BST that are closest to the target.
Follow up:
Assume that the BST is balanced, could you solve it in less than O(n) runtime (where n = total nodes)?

### Solutions
Worst case O(n)
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
    public List<Integer> closestKValues(TreeNode root, double target, int k) {
        List<Integer> result = new LinkedList<Integer>();
        ArrayList<Integer> inorder = new ArrayList<Integer>();
        init(root, inorder);
        double min = Double.MAX_VALUE;
        int index = -1;
        for (int i = 0; i < inorder.size(); i ++) {
            double tmp = inorder.get(i);
            if (Math.abs(tmp - target) < min) {
                min = Math.abs(tmp - target);
                index = i;
            }
        }
        int i = index;
        int j = index;
        while (result.size() < k) {
            System.out.println("i = " + i + "j = " + j);
            if (i == j) {
                result.add(inorder.get(i));
                i --;
                j ++;
                continue;
            }
            double a = Double.MAX_VALUE;
            double b = Double.MAX_VALUE;
            if (i >= 0) {
                a = Math.abs(inorder.get(i) - target);
            }
            if (j< inorder.size()) {
                b = Math.abs(inorder.get(j) - target);
            }
            if (a < b) {
                result.add(inorder.get(i));
                i = i - 1;
            }
            else {
                result.add(inorder.get(j));
                j = j + 1;
            }
        }
        return result;
    }
    private void init(TreeNode root, ArrayList<Integer> inorder) {
        if (root == null) {
            return;
        }
        init(root.left, inorder);
        inorder.add(root.val);
        init(root.right, inorder);
    }
}
```

O(n)
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
    private class Node implements Comparable<Node>{
        public double diff;
        public TreeNode node;
        public Node(double diff, TreeNode node) {
            this.diff = diff;
            this.node = node;
        }
        public int compareTo(Node n) {
            double tmp = this.diff - n.diff;
            if (tmp > 0) {
                return 1;
            }
            else if (tmp < 0) {
                return -1;
            }
            else {
                return 0;
            }
        }
    }
    public List<Integer> closestKValues(TreeNode root, double target, int k) {
        LinkedList<Integer> result = new LinkedList<Integer>();
        PriorityQueue<Node> q = new PriorityQueue<Node>(Collections.reverseOrder());
        inorder(root, q, target, k);
        while (!q.isEmpty()) {
            result.add(q.poll().node.val);
        }
        return result;
    }
    private void inorder(TreeNode node, PriorityQueue<Node> q, double target, int k) {
        if (node == null) {
            return;
        }
        inorder(node.left, q, target, k);
        q.add(new Node(Math.abs(node.val - target), node));
        if (q.size() > k) {
            q.poll();
        }
        inorder(node.right, q, target, k);
    }
}
```

O(k + log(n))
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
    public List<Integer> closestKValues(TreeNode root, double target, int k) {
        LinkedList<Integer> result = new LinkedList<Integer>();
        Stack<TreeNode> pre = new Stack<TreeNode>();
        Stack<TreeNode> suc = new Stack<TreeNode>();
        while(root != null) {
            if (root.val < target) {
                pre.push(root);
                root = root.right;
            }
            else {
                suc.push(root);
                root = root.left;
            }
        }
        while (k > 0) {
            if (suc.isEmpty() || !pre.isEmpty() && target - pre.peek().val < suc.peek().val - target) {
                result.add(pre.peek().val);
                getPre(pre);
            }
            else {
                result.add(suc.peek().val);
                getSuc(suc);
            }
            k --;
        }
        return result;
    }
    private void getPre(Stack<TreeNode> pre) {
        TreeNode node = pre.pop();
        if (node.left != null) {
            pre.push(node.left);
            node = node.left;
            while (node.right != null) {
                pre.push(node.right);
                node = node.right;
            }
        }
    }
    private void getSuc(Stack<TreeNode> suc) {
        TreeNode node = suc.pop();
        if (node.right != null) {
            suc.push(node.right);
            node = node.right;
            while (node.left != null) {
                suc.push(node.left);
                node = node.left;
            }
        }
    }
}
```