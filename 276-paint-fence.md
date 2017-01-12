# 276. Paint Fence

### Problem:

There is a fence with n posts, each post can be painted with one of the k colors.

You have to paint all the posts such that no more than two adjacent fence posts have the same color.

Return the total number of ways you can paint the fence.

Note:
n and k are non-negative integers.

### Solutions:

```java
public class Solution {
    public int numWays(int n, int k) {
        if (n == 0) {
            return 0;
        }
        if (n == 1) {
            return k;
        }
        if (n == 2) {
            return k * k;
        }
        int one = k, two = k * k;
        int result = 0;
        for (int i = 2; i < n; i ++) {
            result = (k - 1) * (one + two);
            one = two;
            two = result;
        }
        return result;
    }
}
```