# 95 Unique Binary Search Trees II – Medium


### Problem:



Given n, generate all structurally unique BST’s (binary search trees) that store values 1…n.

For example,
Given n = 3, your program should return all 5 unique BST’s shown below.

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3

### Thoughts:



Building BST is harder than count the number comparing to the Version I.

Key idea is for a number n

S[1, n] stands for unique binary search trees set from number 1 to n

then use 1 as root, then becomes subproblem(2, n)    Empty set + S[2, n]

then use 2 as root, then becomes subproblem(1,1) * subproblem(3,n)  S[1]  + S[3, n]


### Solutions:
```java
/**
* Definition for a binary tree node.
* public class TreeNode {
* int val;
* TreeNode left;
* TreeNode right;
* TreeNode(int x) { val = x; }
* }
*/
public class Solution {
    public List<TreeNode> generateTrees(int n) {
        if (n == 0) {
            return new LinkedList<TreeNode>();
        }
        return gt(1, n);
    }
    private List<TreeNode> gt(int start, int end){
        List<TreeNode> res = new ArrayList<TreeNode>();
        if (start > end){
            res.add(null);
            return res;
        }
        for (int i = start; i <= end; i ++){
            //use i as root
            List<TreeNode> lefts = gt(start, i - 1);
            List<TreeNode> rights = gt(i + 1, end);
            for (TreeNode left:lefts){
                for (TreeNode right:rights){
                    TreeNode root = new TreeNode(i);
                    root.left = left;
                    root.right = right;
                    res.add(root);
                }//for right
            }//for left
        }//for i
        return res;
    }
}
```
