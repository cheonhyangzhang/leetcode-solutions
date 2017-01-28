# 371 Sum of Two Integers

### Problem:

Calculate the sum of two integers a and b, but you are not allowed to use the operator + and -.

Example:
Given a = 1 and b = 2, return 3.

### Solutions:

```java
public class Solution {
    public int getSum(int a, int b) {
        while (a != 0 && b != 0) {
            int and = a & b;
            int xor = a ^ b;
            a = and << 1;
            b = xor;
        }
        if (a!= 0) {
            return a;
        }
        else {
            return b;
        }
    }
}
```