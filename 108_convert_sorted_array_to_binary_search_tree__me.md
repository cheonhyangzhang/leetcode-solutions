# 108 Convert Sorted Array to Binary Search Tree – Medium


### Problem:



Given an array where elements are sorted in ascending order, convert it to a height balanced BST.


### Thoughts:



This is very modified binary search question.

Always picking the mid value of a sorted array to be the root for a binary search tree is a good choice since this will create a balanced BST.


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
    public TreeNode sortedArrayToBST(int[] nums) {
        if (nums.length == 0){
            return null;
        }
        return buildBST(nums, 0, nums.length - 1);
    }
    private TreeNode buildBST(int[] nums, int start, int end){
        if (start > end)
            return null;
        else{
            int mid = ( start + end ) / 2;
            TreeNode node = new TreeNode(nums[mid]);
            node.left = buildBST(nums, start, mid - 1);
            node.right = buildBST(nums, mid + 1, end);
            return node;
        }
    }
}
```