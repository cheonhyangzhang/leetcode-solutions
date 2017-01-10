# 255. Verify Preorder Sequence in Binary Search Tree - Medium

### Problem:
<pre>
Given an array of numbers, verify whether it is the correct preorder traversal sequence of a binary search tree.

You may assume each number in the sequence is unique.

Follow up:
Could you do it using only constant space complexity?
</pre>

### Solutions:
```java
public class Solution {
    public boolean verifyPreorder(int[] preorder) {
        if (preorder.length == 0) {
            return true;
        }
        return vp(preorder, 0, preorder.length - 1);
    }
    private boolean vp(int[] pre, int left, int right) {
        if (left >= right) {
            return true;
        }
        int i = left + 1;
        while (i <= right) {
            if (pre[i] > pre[left]) {
                break;
            }
            i ++;
        }
        if (i > right) {
            return vp(pre, left + 1, right);
        }
        int cut = i - 1;
        while (i <= right) {
            if (pre[i] < pre[left]) {
                return false;
            }
            i ++;
        }
        return vp(pre, left + 1, cut) && vp(pre, cut + 1, right);
    }
}
```
```java

```