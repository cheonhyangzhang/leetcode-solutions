# 255. Verify Preorder Sequence in Binary Search Tree -  Medium

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
        int low = Integer.MIN_VALUE;
        Stack<Integer> stack = new Stack<Integer>();
        for (int i = 0; i < preorder.length; i ++) {
            if (preorder[i] < low) {
                return false;
            }
            while(stack.size() > 0 && preorder[i] > stack.peek()) {
                low = stack.pop();
            }
            stack.push(preorder[i]);
        }
        return true;
    }
}
```

```java
public class Solution {
    public boolean verifyPreorder(int[] preorder) {
        int low = Integer.MIN_VALUE;
        int index = -1;
        for (int i = 0; i < preorder.length; i ++) {
            if (preorder[i] < low) {
                return false;
            }
            while (index >= 0 && preorder[i] > preorder[index]) {
                low = preorder[index--];
            }
            preorder[++index] = preorder[i];
        }
        return true;
    }
}
```