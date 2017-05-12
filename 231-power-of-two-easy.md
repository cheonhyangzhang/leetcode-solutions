# 231 Power of Two – Easy

### Problem:
Given an integer, write a function to determine if it is a power of two.

### Thoughts:
The most straightforward is to use a recursion way. As shown in the first solution below. The running time of this solution will depends on how large the given Integer is, because for a number, 2^m, the running time will be (m).

The second solution is based on bit manipulation. Because if one integer is the power of two, it must starts with 1 and end with all trailing 0.
So we can use a mask that starts with 10000…0 (31 0s), use & operation to find the first 1. Then we use ~ to get the opposite of the mask, e.g 00001000…00 will becomes 11110111…11, and use & with given integer, if given Integer is the power of 2, the result of & should be 0. This solution will run at most 32 iteration, so it’s O(1) time. This is better solution.

### Solutions:

```java
public class Solution {
    public boolean isPowerOfTwo(int n) {
        if (n <= 0) {
            return false;
        }
        if (n == 1) {
            return true;
        }
        if (n % 2 != 0) {
            return false;
        }
        return isPowerOfTwo(n / 2);
    }
}
```

```java
public class Solution {
    public boolean isPowerOfTwo(int n) {
        if (n <= 0) {
            return false;
        }
        if (n == 1) {
            return true;
        }
        int mask = 1 << 31;
        for (int i = 0; i >> 1;
        }
        if ((n&(~mask)) == 0) {
            return true;
        }
        else {
            return false;
        }
    }
}
```